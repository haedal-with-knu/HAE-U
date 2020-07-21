# 테트리스 만들기3

## 수업내용

- 이동 범위 한정하기
    - 경계 안에서 움직이게 하기
- 바닥에 닿을 경우 처리
    - 구현 순서 구상하기
    - 행 노드를 이용하여 관리하기
    - 바닥에 닿았을 경우 해당 위치에 고정하기
    - 이동 가능 조건 변경
    - 바닥까지 한번에 이동기능 추가하기

# 이동 범위 한정하기

## **경계 안에서 움직이게 하기**

- 테트로미노는 앞서 만들어 둔 배경 타일 안에서 움직여야  합니다. 따라서 배경 타일 밖으로 벗어나지 못하도록 해야 합니다.
- 일단 이동 또는 회전한 뒤, 그 좌표가 경계 안인지 확인 후 경계 밖이라면 조금 전 실행을 취소하는 방법을 이용해 보겠습니다.

```csharp
using UnityEngine;
public class Stage : MonoBehaviour
{
		...

    private void Start()
    {
     ...
    }

    void Update()   // 매 프레임마다 실행
    {
     ...
    }

    // 이동이 가능한지 체크후 True or False 반환하는 메서드
    bool MoveTetromino(Vector3 moveDir, bool isRotate)
    {
        //이동 or 회전 불가시 돌아가기 위한 값 저장
        Vector3 oldPos = tetrominoNode.transform.position; 
        Quaternion oldRot = tetrominoNode.transform.rotation;

        //이동 & 회전 하기
        tetrominoNode.transform.position += moveDir;
        if (isRotate)
        {
            //현재 테트로미노 노드에 90도 회전을 더해 줌.
            tetrominoNode.transform.rotation *= Quaternion.Euler(0, 0, 90);
        }

        // 이동 불가시 이전 위치, 회전 으로 돌아가기
        if (!CanMoveTo(tetrominoNode))
        {
            tetrominoNode.transform.position = oldPos;
            tetrominoNode.transform.rotation = oldRot;

            return false;
        }

        return true;
    }

    // 이동 가능한지 체크 후 True or False 반환하는 메서드
    bool CanMoveTo(Transform root)  //tetrominoNode를 매개변수 root로 가져오기
    {
        //tetrominoNode의 자식 타일을 모두 검사
        for (int i = 0; i < root.childCount; ++i)  
        {
            var node = root.GetChild(i);

            //유니티 좌표계에서 테트리스 좌표계로 변환
            int x = Mathf.RoundToInt(node.transform.position.x + halfWidth);
            int y = Mathf.RoundToInt(node.transform.position.y + halfHeight - 1);

            //이동 가능한 좌표인지 확인 후 반환
            if (x < 0 || x > boardWidth - 1)
                return false;
            if (y < 0)
                return false;

        }
        return true;
    }

    // 타일 생성
    Tile CreateTile(Transform parent, Vector2 position, Color color, int order = 1)
    {
		 ...
    }

    // 배경 타일을 생성
    void CreateBackground()
    {
     ...
    }
    // 테트로미노 생성
    void CreateTetromino()
    {
     ...
    }
}
```

### 주의사항

- 좌표계 변환시 y값 설정 주의하기. 배경을 만들때 타일을 배치한 방식을 고려하여 세로 변환시 1 더 빼주기

![3%20ec67741c46f945b094bbb2ccdabd0e23/Untitled.png](3%20ec67741c46f945b094bbb2ccdabd0e23/Untitled.png)

# **바닥에 닿을 경우 처리**

## 구현 순서 구상하기

### **1) 바닥에 닿으면 해당 위치 고정**

테트로미노 노드의 타일을 보드 노드로 옮기기

### **2) 가로 행에 빈틈없이 가득 차면 해당 행 삭제**

해당 행의 타일 개수가 width와 같으면 해당 타일 삭제

### **3) 빈 행이 없도록 아래로 떨어뜨림**

모든 행들을 살펴보면서 아래가 비어 있으면 아래로 내리기

### **4) 새로운 테트로미노 생성 후 다시 시작**

위의 행동이 끝난 이후 **CreateTetromino 메서드** 호출 ****

## 행 노드를 이용하여 관리하기

### 행 노드 만들기

 이를 구현하기 위해선 행을 구분할 수 있어야 합니다. 먼저 보드 노드의 자녀들로 행 노드들을 만들어 별도로 관리해보겠습니다. 관리를 쉽게 하기 위해 행 노드의 이름은 테트리스 좌표계 기준으로 행 노드의 y 값으로 설정하겠습니다.

```csharp
private void Start()
    {
        ...
        CreateBackground();

        // 높이만큼 행 노드 만들어주기
        for (int i = 0; i < boardHeight; ++i)
        {
						// ToString을 이용하여 오브젝트 이름 설정
            var col = new GameObject((boardHeight - i - 1).ToString());
            // 위치설정 -> 행 위치의 높이, 가로 중앙
            col.transform.position = new Vector3(0, halfHeight - i, 0);
            // 보드 노드의 자식으로 설정
            col.transform.parent = boardNode;
        }

        CreateTetromino();
    }
```

위와 같이 행 노드를 만들어 준 후 게임을 실행시키면 다음과 같이 행 노드들이 만들어집니다.

![3%20ec67741c46f945b094bbb2ccdabd0e23/Untitled%201.png](3%20ec67741c46f945b094bbb2ccdabd0e23/Untitled%201.png)

### 바닥에 닿았을 경우

바닥에 닿았을 경우에 대한 코드를 작성해 봅시다. 이동 불가하고 현재 아래로 떨어지고 있다면 바닥에 닿았다고 판단해보겠습니다.

```csharp
bool MoveTetromino(Vector3 moveDir, bool isRotate)
    {
        ...

				// 이동 불가시 이전 위치, 회전 으로 돌아가기
        if (!CanMoveTo(tetrominoNode))
        {
            tetrominoNode.transform.position = oldPos;
            tetrominoNode.transform.rotation = oldRot;

            //바닥에 닿았다는 의미 = 이동 불가하고 현재 아래로 떨어지고 있는 상황
            if ((int)moveDir.y == -1 && (int)moveDir.x == 0 && isRotate == false)
            {
                AddToBoard(tetrominoNode);
                CheckBoardColumn();
                CreateTetromino();
            }

            return false;
        }

        return true;
    }

    // 테트로미노를 보드에 추가
    void AddToBoard(Transform root)
    {

    }

    // 보드에 완성된 행이 있으면 삭제
    void CheckBoardColumn()
    {

    }
```

## **바닥에 닿았을 경우 해당 위치에 고정하기**

 위의 코드에 이어서 **AddToBoard 메서드**를 작성해보겠습니다. 테트로미노가 바닥에 닿을시 테트로미노의 자녀 오브젝트들의 부모 노드를 Board 노드로 바꾸어 오브젝트들이 이동할 수 있게 하였습니다. 또한 자녀 오브젝트들의 이름을 유니티 좌표계 기준 x 위치로 만들어 나중에 관리하기 쉽게 만들었습니다.

```csharp
		// 테트로미노를 보드에 추가
    void AddToBoard(Transform root) //tetrominoNode를 매개변수 root로 가져오기
    {
        while (root.childCount > 0)
        {
            var node = root.GetChild(0);

            //유니티 좌표계에서 테트리스 좌표계로 변환
            int x = Mathf.RoundToInt(node.transform.position.x + halfWidth);
            int y = Mathf.RoundToInt(node.transform.position.y + halfHeight - 1);

            //부모노드 : 행 노드(y 위치), 오브젝트 이름 : x 위치
            node.parent = boardNode.Find(y.ToString());
            node.name = x.ToString();
        }
    }
```

위의 코드 실행 결과입니다. 위치에 알맞은 행 오브젝트와 그 자녀 오브젝트 이름이 설정된 것을 확인할 수 있습니다.

![3%20ec67741c46f945b094bbb2ccdabd0e23/Untitled%202.png](3%20ec67741c46f945b094bbb2ccdabd0e23/Untitled%202.png)

### 자식타일 확인 방법들

**1) 일반적으로 자식 타일 확인할 경우**

![3%20ec67741c46f945b094bbb2ccdabd0e23/Untitled%203.png](3%20ec67741c46f945b094bbb2ccdabd0e23/Untitled%203.png)

**2) 자식 타일을 다른곳으로 이동시킬 경우 (자식 타일이 모두 없어질때까지 반복)**

![3%20ec67741c46f945b094bbb2ccdabd0e23/Untitled%204.png](3%20ec67741c46f945b094bbb2ccdabd0e23/Untitled%204.png)

![3%20ec67741c46f945b094bbb2ccdabd0e23/Untitled%205.png](3%20ec67741c46f945b094bbb2ccdabd0e23/Untitled%205.png)

## **이동 가능 조건 변경하기**

테트리스 경우 바닥에 닿았을 때만 보드가 쌓이는 것이 아닌 다른 테트리스 노드에 닿았을 경우도 멈추어야 합니다. 따라서 바닥에 닿았을 경우뿐 아니라 이미 다른 타일이 존재할 경우도 이동 가능 조건에 추가해주어야 합니다. **CanMoveTo 메서드**를 수정해봅시다.

```csharp
// 이동 가능한지 체크 후 True or False 반환하는 메서드
    bool CanMoveTo(Transform root)  // tetrominoNode를 매개변수 root로 가져오기
    {
        // tetrominoNode의 자식 타일을 모두 검사
        for (int i = 0; i < root.childCount; ++i)  
        {
            var node = root.GetChild(i);
            // 유니티 좌표계에서 테트리스 좌표계로 변환
            int x = Mathf.RoundToInt(node.transform.position.x + halfWidth);
            int y = Mathf.RoundToInt(node.transform.position.y + halfHeight - 1);
            // 이동 가능한 좌표인지 확인 후 반환
            if (x < 0 || x > boardWidth - 1)
                return false;
            if (y < 0)
                return false;

            // 이미 다른 타일이 있는지 확인
            var column = boardNode.Find(y.ToString());

            if (column != null && column.Find(x.ToString()) != null)
                return false;
        }
        return true;
    }
```

## **바닥까지 한번에 이동기능 추가하기**

바닥까지 한 번에 이동하도록 구현해봅시다. (spacebar 이용) 기존 메서드와 while을 이용하여 손쉽게 구현할 수 있습니다. 또한 재시작을 쉽게 하기 위해 재시작 키를 추가해봅시다. (키보드 r 이용).

```csharp
void Update()   // 매 프레임마다 실행
    {
         ...

        else if (Input.GetKeyDown("s"))
        {
            moveDir.y = -1;
        }

        if (Input.GetKeyDown("space"))
        {
            // 테트로미노가 바닥에 닿을 때까지 아래로 이동
            while (MoveTetromino(Vector3.down, false))
            {
            }
        }

        if (Input.GetKeyDown("r"))
        {
            // SceneManager을 이용하여 게임 재시작하기
						// 가장 위에 using UnityEngine.SceneManagement; 추가 필요
            SceneManager.LoadScene(SceneManager.GetActiveScene().buildIndex);
        }

        // 아래로 떨어지는 경우는 강제로 이동시킵니다.
        if (Time.time > nextFallTime)

				 ...

    }
```

### SceneManager

- 유니티에서 Scene(맵)을 이동이나 재시작을 관리하는 매니저입니다.

## 현재까지 작업결과입니다.

[테트리스 만들기 3](https://drive.google.com/file/d/1nydTaSlYDQQcqPIIHp5KuxDGy5gFWerI/view?usp=sharing)