# 테트리스 만들기 2

---

## 수업내용

- 타일 관리시스템 구현
    - 타일 생성기능 만들기
    - 배경 그리기
- 테트로미노 생성과 관리
    - 테트로미노 만들기
    - 테트로미노의 이동 구현
    - 자동으로 아래로 떨어지게 하기

    ---

## 타일 관리시스템 구현

### **타일 생성기능 만들기**

```csharp
using UnityEngine;

public class Stage : MonoBehaviour
{
    ... //앞의 내용 뒤에 이어서 적기

    // 타일 생성
    Tile CreateTile(Transform parent, Vector2 position, Color color, int order = 1)
    {
        var go = Instantiate(tilePrefab); // tilePrefab를 복제한 오브젝트 생성
        go.transform.parent = parent; // 부모 지정
        go.transform.localPosition = position; // 위치 지정

        var tile = go.GetComponent<Tile>(); // tilePrefab의 Tile스크립트 불러오기
        tile.color = color; // 색상 지정
        tile.sortingOrder = order; // 순서 지정

        return tile;
    }
}
```

var 을 이용하여 Instantiate(tilePrefab)을 간단한 go 라는 변수로 바꾸어 주고 활용하였습니다.

### **배경 그리기**

```csharp
using UnityEngine;

public class Stage : MonoBehaviour
{

    ... 

    private int halfWidth;
    private int halfHeight;

    private void Start() // 게임이 시작되고 한 번만 실행
    {
        halfWidth = Mathf.RoundToInt(boardWidth * 0.5f);    // 너비의 중간값 설정해주기
        halfHeight = Mathf.RoundToInt(boardHeight * 0.5f);   // 높이의 중간값 설정해주기

        CreateBackground(); // 배경 만들기
    }

    // 타일 생성
    Tile CreateTile(Transform parent, Vector2 position, Color color, int order = 1)
    {
     ... 
    }

    // 배경 타일을 생성
    void CreateBackground()
    {
        Color color = Color.gray;   // 배경 색 설정(원하는 색으로 설정 가능)

        // 타일 보드
        color.a = 0.5f; // 테두리와 구분 위해 투명도 바꾸기
        for (int x = -halfWidth; x < halfWidth; ++x)    
        {
            for (int y = halfHeight; y > -halfHeight; --y)
            {
                CreateTile(backgroundNode, new Vector2(x, y), color, 0);
            }
        }

        // 좌우 테두리
        color.a = 1.0f;
        for (int y = halfHeight; y > -halfHeight; --y)
        {
            CreateTile(backgroundNode, new Vector2(-halfWidth - 1, y), color, 0);
            CreateTile(backgroundNode, new Vector2(halfWidth, y), color, 0);
        }

        // 아래 테두리
        for (int x = -halfWidth - 1; x <= halfWidth; ++x)
        {
            CreateTile(backgroundNode, new Vector2(x, -halfHeight), color, 0);
        }
    }
```

테두리 및 배경 타일 생성시 위치 범위 잘 생각해주면서 for문 범위 설정해주기.

![2%209bc0299a385e4e6db69df8c7cb6f7acb/Untitled.png](2%209bc0299a385e4e6db69df8c7cb6f7acb/Untitled.png)

---

## 테트로미노 생성과 관리

### **테트로미노 만들기**

![2%209bc0299a385e4e6db69df8c7cb6f7acb/Untitled%201.png](2%209bc0299a385e4e6db69df8c7cb6f7acb/Untitled%201.png)

테트리스는 4개의 타일로 구성된 블록을 사용하는 게임으로, 테트리스 컴퍼니의 세계 표준 색상과 모양을 사용해보겠습니다. (나중에 이를 활용하여 새로운 모양을 만들거나 원하는 색을 적용할 수 있습니다)

```csharp
using UnityEngine;

public class Stage : MonoBehaviour
{
    ...

    private void Start()
    {
        ...

        CreateTetromino(); // 테트로미노 만들기
    }

    ...

    // 테트로미노 생성
    void CreateTetromino()
    {
        int index = Random.Range(0, 7); // 랜덤으로 0~6 사이의 값 생성
        //위의 코드 대신 아래와 같은 코드로 원하는 Index모양 확인 가능
        //int index = 1; 

        Color32 color = Color.white;

				// 회전 계산에 사용하기 위한 쿼터니언 클래스
        tetrominoNode.rotation = Quaternion.identity;    
				// 테트로미노 생성 위치 (중앙 상단)
        tetrominoNode.position = new Vector2(0, halfHeight);   

        switch (index)
        {
            // 구분을 위해 테트리스 모양에 비슷하게 영어로 표현 (I, J, L ,O, S, T, Z)

            case 0: // I
                color = new Color32(115, 251, 253, 255);    // 하늘색
                CreateTile(tetrominoNode, new Vector2(-2f, 0.0f), color);
                CreateTile(tetrominoNode, new Vector2(-1f, 0.0f), color);
                CreateTile(tetrominoNode, new Vector2(0f, 0.0f), color);
                CreateTile(tetrominoNode, new Vector2(1f, 0.0f), color);
                break;

            case 1: // J
                color = new Color32(0, 33, 245, 255);    // 파란색
                CreateTile(tetrominoNode, new Vector2(-1f, 0.0f), color);
                CreateTile(tetrominoNode, new Vector2(0f, 0.0f), color);
                CreateTile(tetrominoNode, new Vector2(1f, 0.0f), color);
                CreateTile(tetrominoNode, new Vector2(-1f, 1.0f), color);
                break;

            case 2: // L
                color = new Color32(243, 168, 59, 255);    // 주황색
                CreateTile(tetrominoNode, new Vector2(-1f, 0.0f), color);
                CreateTile(tetrominoNode, new Vector2(0f, 0.0f), color);
                CreateTile(tetrominoNode, new Vector2(1f, 0.0f), color);
                CreateTile(tetrominoNode, new Vector2(1f, 1.0f), color);
                break;

            case 3: // O 
                color = new Color32(255, 253, 84, 255);    // 노란색
                CreateTile(tetrominoNode, new Vector2(0f, 0f), color);
                CreateTile(tetrominoNode, new Vector2(1f, 0f), color);
                CreateTile(tetrominoNode, new Vector2(0f, 1f), color);
                CreateTile(tetrominoNode, new Vector2(1f, 1f), color);
                break;

            case 4: //  S
                color = new Color32(117, 250, 76, 255);    // 녹색
                CreateTile(tetrominoNode, new Vector2(-1f, -1f), color);
                CreateTile(tetrominoNode, new Vector2(0f, -1f), color);
                CreateTile(tetrominoNode, new Vector2(0f, 0f), color);
                CreateTile(tetrominoNode, new Vector2(1f, 0f), color);
                break;

            case 5: //  T
                color = new Color32(155, 47, 246, 255);    // 자주색
                CreateTile(tetrominoNode, new Vector2(-1f, 0f), color);
                CreateTile(tetrominoNode, new Vector2(0f, 0f), color);
                CreateTile(tetrominoNode, new Vector2(1f, 0f), color);
                CreateTile(tetrominoNode, new Vector2(0f, 1f), color);
                break;

            case 6: // Z
                color = new Color32(235, 51, 35, 255);    // 빨간색
                CreateTile(tetrominoNode, new Vector2(-1f, 1f), color);
                CreateTile(tetrominoNode, new Vector2(0f, 1f), color);
                CreateTile(tetrominoNode, new Vector2(0f, 0f), color);
                CreateTile(tetrominoNode, new Vector2(1f, 0f), color);
                break;
        }
    }
}
```

테트로미노에서 원점(0,0)을 기준으로 상대좌표 이용하여 원하는 모양 만들기

![2%209bc0299a385e4e6db69df8c7cb6f7acb/Untitled%202.png](2%209bc0299a385e4e6db69df8c7cb6f7acb/Untitled%202.png)

실행하여 제작한 모양이 잘 나오는지 확인할 수 있습니다.

### **테트로미노 이동 구현**

키보드의 w, a, s, d와 space를 이용하여 테트로미노를 컨트롤 할 수 있도록 해보겠습니다.

![2%209bc0299a385e4e6db69df8c7cb6f7acb/Untitled%203.png](2%209bc0299a385e4e6db69df8c7cb6f7acb/Untitled%203.png)

먼저 w,a,s,d를 입력받고 그에 따른 행동을 구현해보겠습니다.

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
				//초기화
        Vector3 moveDir = Vector3.zero; //이동 여부 저장용
        bool isRotate = false;  // 회전 여부 저장용

        //각 키에 따라 이동 여부 혹은 회전 여부를 설정해줍니다.
        if (Input.GetKeyDown("a"))  
        {
            moveDir.x = -1;

        }
        else if (Input.GetKeyDown("d"))
        {
            moveDir.x = 1;
        }

        if (Input.GetKeyDown("w"))
        {
            isRotate = true;
        }
        else if (Input.GetKeyDown("s"))
        {
            moveDir.y = -1;
        }

        // 아무런 키 입력이 없을경우 Tetromino 움직이지 않게하기
        if (moveDir != Vector3.zero || isRotate)
        {
            MoveTetromino(moveDir, isRotate);
        }
    }

    // 이동이 가능하면 true, 불가능하면 false를 return
    bool MoveTetromino(Vector3 moveDir, bool isRotate)
    {
        tetrominoNode.transform.position += moveDir;
        if (isRotate)
        {
            //현재 테트로미노 노드에 90도 회전을 더해 줌.
            tetrominoNode.transform.rotation *= Quaternion.Euler(0, 0, 90);
        }
        return true;
    }

    // 타일 생성
    ...
}
```

### **자동으로 아래로 떨어지게 하기**

```csharp
using UnityEngine;

public class Stage : MonoBehaviour
{
    ...
    private float nextFallTime; // 다음에 테트로미노가 떨어질 시간을 저장

    private void Start()
    {
				halfWidth = Mathf.RoundToInt(boardWidth * 0.5f);
        halfHeight = Mathf.RoundToInt(boardHeight * 0.5f);

        nextFallTime = Time.time + fallCycle;   // 다음에 테트로미노가 떨어질 시간 설정

        CreateBackground();

        CreateTetromino();
    }

    void Update()
    {
        ...
        // 아래로 떨어지는 경우는 강제로 이동시킵니다.
        if (Time.time > nextFallTime)
        {
						nextFallTime = Time.time + fallCycle;   // 다음 떨어질 시간 재설정
            moveDir.y = -1; //  아래로 한 칸 이동
            isRotate = false;   // 강제로 이동시 회전 없음
        }

        // 아무런 키 입력이 없을경우 Tetromino 움직이지 않게하기
        if (moveDir != Vector3.zero || isRotate)
        {
            MoveTetromino(moveDir, isRotate);
        }
    }
}
```

---

### 현재까지 작업결과입니다.

[테트리스 만들기 2](https://drive.google.com/file/d/1TgfFrbnFZbJtRRrw29tNTssnREvU9mVu/view?usp=sharing)