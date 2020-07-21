# 테트리스 만들기 4

## 수업내용

- 완료된 행 처리하기
    - 완성된 행 삭제하기
    - 삭제된 행 위의 노드 아래로 내리기
- 게임오버 처리
    - 게임오버 UI 추가하기
    - UI 관리 스크립트 작성하기

# **완성된 행 처리하기**

## 완성된 행 삭제하기

보드 노드에 추가한 행 노드를 활용하여 행이 완성되었는지 확인하고 해당 행을 삭제할 수 있습니다. 행 완성 여부는 행 노드의 자녀 개수와 boardwidth를 비교하여 확인합니다. 행이 완성되었다면, Destroy와 DetachChildren 기능을 이용하여 행의 자녀들을 모두 삭제해줍니다.

```csharp
// 보드에 완성된 행이 있으면 삭제
    void CheckBoardColumn()
    {
        bool isCleared = false;

        // 완성된 행 == 행의 자식 갯수가 가로 크기
        foreach (Transform column in boardNode)
        {
            if (column.childCount == boardWidth)
            {
                //행의 모든 자식을 삭제
                foreach (Transform tile in column)
                {
                    Destroy(tile.gameObject);
                }
                // 행의 모든 자식들과의 연결 끊기
                column.DetachChildren();
                isCleared = true;
            }
        }
    }
```

이번에는 for문이 아닌 foreach문을 이용하여 자식관계를 표현하고 활용해 보았습니다. 

### foreach

- 끝을 지정해주는 다른 반복문과 달리, 인자로 들어온 item의 내부 인덱스를 처음부터 끝까지 알아서 순환을 해주는 반복문입니다.

### foreach vs for문

foreach를 앞에서의 방법인 for문을 이용하여 아래와 같이 표현할 수 ㅣ있습니다.

![4%20822aadd0f2e0460491a1f2268f84e1cc/Untitled.png](4%20822aadd0f2e0460491a1f2268f84e1cc/Untitled.png)

 위의 코드 실행 결과, 다음과 같이 완성된 행이 잘 지워지는 것을 확인할 수 있습니다. 하지만 행이 지워지기만 하고 빈칸이 채워지지 않아 아직 부자연스럽습니다. 이제부턴 행이 삭제되면 빈칸을 없애주는 작업을 해보겠습니다.

![4%20822aadd0f2e0460491a1f2268f84e1cc/Untitled%201.png](4%20822aadd0f2e0460491a1f2268f84e1cc/Untitled%201.png)

## 삭제된 행 위의 노드 아래로 내리기

 행이 삭제되면 위의 노드들을 빈칸만큼 아래로 내려야 합니다. 다양한 경우를 가정하고 코드를 작성해야 합니다.

![4%20822aadd0f2e0460491a1f2268f84e1cc/Untitled%202.png](4%20822aadd0f2e0460491a1f2268f84e1cc/Untitled%202.png)

**1.** 1개 행이 사라진 경우, 1행을 0행으로, 2행을 1행으로 1칸씩 내려줘야 합니다.

**2.** 3행을 0행으로, 4행으로 2행으로 3칸 내려줘야 합니다.

**3.** 1행을 0행으로, 3행을 1행으로 각각 1칸, 2칸 내려줘야 합니다.

위의 상황들을 모두 고려해서 코딩을 해보겠습니다.

```csharp
// 보드에 완성된 행이 있으면 삭제
    void CheckBoardColumn()
    {

			...

        // 비어 있는 행이 존재하면 아래로 내리기
        if (isCleared)
        {
            //가장 바닥 행은 내릴 필요가 없으므로 index 1 부터 for문 시작
            for (int i = 1; i < boardNode.childCount; ++i)
            {
                var column = boardNode.Find(i.ToString());

                // 이미 비어 있는 행은 무시
                if (column.childCount == 0)
                    continue;

                // 현재 행 아래쪽에 빈 행이 존재하는지 확인, 빈 행만큼 emptyCol 증가
                int emptyCol = 0;
                int j = i - 1;
                while (j >= 0)
                {
                    if (boardNode.Find(j.ToString()).childCount == 0)
                    {
                        emptyCol++;
                    }
                    j--;
                }

                // 현재 행 아래쪽에 빈 행 존재시 아래로 내림
                if (emptyCol > 0)
                {
                    var targetColumn = boardNode.Find((i - emptyCol).ToString());

                    while (column.childCount > 0)
                    {
                        Transform tile = column.GetChild(0);
                        tile.parent = targetColumn;
                        tile.transform.position += new Vector3(0, -emptyCol, 0);
                    }
                    column.DetachChildren();
                }
            }
        }
    }
```

### 주의사항

- 위의 코드에서 비어있는 행을 확인할 때 **아래서부터 위로** 검사해 나가야 합니다. 그렇지 않으면 코드가 충돌하여 원하지 않는 결과가 나올 수 있습니다.

# **게임오버 처리하기**

 마지막으로 게임오버를 체크 후 게임 재시작 기능을 만들어 보겠습니다. 게임오버의 조건은 새로운 테트로미노를 생성했을 때 해당 위치에 이미 다른 타일이 존재할 때로 설정해보았습니다.

## 게임오버 UI 추가하기

 게임오버 표시를 위하여 UI > Panel 로 Panel을 만든 후 **Panel** 이라 이름을 정해줍니다.

![4%20822aadd0f2e0460491a1f2268f84e1cc/Untitled%203.png](4%20822aadd0f2e0460491a1f2268f84e1cc/Untitled%203.png)

Panel 에 자식 오브젝트로 UI > Text 를 추가해준 후 **Label**이라 이름을 정해줍니다.

![4%20822aadd0f2e0460491a1f2268f84e1cc/Untitled%204.png](4%20822aadd0f2e0460491a1f2268f84e1cc/Untitled%204.png)

그 후 원하는 글자를 Text 메뉴를 이용하여 적어줍니다. 예시에선 **GameOver**이라 텍스트를 설정해주었습니다.

![4%20822aadd0f2e0460491a1f2268f84e1cc/Untitled%205.png](4%20822aadd0f2e0460491a1f2268f84e1cc/Untitled%205.png)

## UI관리 스크립트 작성하기

이제 이 Panel을 컨트롤 할 수 있게 코드를 작성해 봅시다.

먼저 Panel을 불러올 수 있도록 유니티에디터를 수정해 줍니다.

```csharp
using UnityEngine;
using UnityEngine.SceneManagement;
public class Stage : MonoBehaviour
{
    //필요 소스 불러오기
    [Header("Source")]
    public GameObject tilePrefab;
    public Transform backgroundNode;
    public Transform boardNode;
    public Transform tetrominoNode;
    public GameObject gameoverPanel;

 ...
```

에디터로 돌아와서 "Canvas/Panel" 을 연결해줍니다.

![4%20822aadd0f2e0460491a1f2268f84e1cc/Untitled%206.png](4%20822aadd0f2e0460491a1f2268f84e1cc/Untitled%206.png)

게임 시작시 Panel이 꺼져있어야 하므로 Start메서드에 코드를 추가해줍니다.

```csharp
private void Start()
    {
        // 게임 시작시 게임오버 패널 off
        gameoverPanel.SetActive(false);

				...
```

 

이후 **MoveTetromino 메서드**에 테트로미노 추가 직후 이동 가능 여부 확인 코드를 추가해줍니다. 이전 위치, 회전으로 돌아가도 여전히 움직일 수 없는 상태일 경우 게임 오버 상태로 판단할 예정입니다.

```csharp
		bool MoveTetromino(Vector3 moveDir, bool isRotate)
    {
     ...
        // 이동 불가시 이전 위치, 회전 으로 돌아가기
        if (!CanMoveTo(tetrominoNode))
        {
         ...
            //바닥에 닿았다는 의미 = 이동 불가하고 현재 아래로 떨어지고 있는 상황
            if ((int)moveDir.y == -1 && (int)moveDir.x == 0 && isRotate == false)
            {
                AddToBoard(tetrominoNode);
                CheckBoardColumn();
                CreateTetromino();

                //테트로미노 새로 추가 직후 이동 가능 확인
                if (!CanMoveTo(tetrominoNode))
                {
                    gameoverPanel.SetActive(true);
                }
            }
            return false;
        }
        return true;
    }
```

 마지막으로 **update 메서드** 에서 게임오버 상태와 게임 상태를 구분할 수 있는 코드를 추가해주면 됩니다. 예시에선 gameoverPanel의 작동 상태에 따라 게임 처리 상태를 구분하였지만, 변수를 추가하여 게임 처리 상태를 구분하는 것도 좋습니다.

```csharp
void Update()   // 매 프레임마다 실행
    {
        // 게임오버 처리
        if (gameoverPanel.activeSelf)
        {
            if (Input.GetKeyDown("r"))
            {
                SceneManager.LoadScene(0);
            }
        }
        // 게임 처리
        else
        {
            //초기화
            Vector3 moveDir = Vector3.zero; //이동 여부 저장용
            bool isRotate = false;  // 회전 여부 저장용
				
						...
           
        }
    }
```

게임오버시 keyboard 'r '을 이용하여 게임을 재시작 할 수 있게 하였습니다.

## 현재까지 작업결과입니다.

[테트리스 만들기 4](https://drive.google.com/file/d/1WviA56Oy57ZTeFowXR9KhKvLTOqgmRtS/view?usp=sharing)