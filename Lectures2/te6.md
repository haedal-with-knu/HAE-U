# 테트리스 만들기 6

## 수업내용

- 2인용 게임 구상하기
    - 활용방안 생각하기
    - Hierarchy 수정하기
- 2P용 스크립트 작성하기
    - 사전설정
    - 2P 위치 조정하기
    - 2P용 키 할당하기
    - 보완하기
- 2인용 게임 완성하기
    - 레벨 디자인 수정하기
    - 게임오버 조건 수정하기
- 기타 활용 방안 생각해보기

# 2인용 게임 구상하기

## 활용방안 생각하기

 지금까지 배운 기술들을 이용하여 다양하게 활용할 수 있습니다. 예시에선 친구와 같이 플레이할 수 있는 2인용 게임을 만들어보겠습니다.

 역시나 코드를 작성하기 전에 UI 배치 구상도를 미리 생각해보는 것이 좋습니다.

![6%20a9208a54bb7649559f2fcafbc940f0e5/Untitled.png](6%20a9208a54bb7649559f2fcafbc940f0e5/Untitled.png)

 

새로운 플레이어가 추가되었으므로 추가로 필요한 키도 생각해줍니다.

![6%20a9208a54bb7649559f2fcafbc940f0e5/Untitled%201.png](6%20a9208a54bb7649559f2fcafbc940f0e5/Untitled%201.png)

 이제 수정해야할것을 정리해봅시다.

### 수정 필요사항

- 새로운 플레이어(2P)를 위한 새로운 오브젝트 Stage2, Board, BG, Tetromino가 필요합니다.
- 새로운 플레이어(2P)를 위한 새로운 UI 오브젝트 Score2, Level2, Line2가 필요합니다.
- 이미 있는 코드와 노드들을 최대한 활용하기 위해 Stage.cs 스크립트를 그대로 사용하여 Stage2.cs를 제작할 예정입니다.
- 2P의 BG 및 테트로미노가 겹치면 안되므로 Stage2.cs에서 x 값 조정이 필요합니다.

## Hierarchy 수정하기

 두번째 플레이어를 위한 Stage 오브젝트를 만들어봅시다. 간단하게 ctrl+c, ctrl+v를 이용하여 Stage와 똑같은 오브젝트를 만들어낼 수 있습니다. 새로만든 Stage복사본의 이름을 **Stage2**로 정해줍니다.

![6%20a9208a54bb7649559f2fcafbc940f0e5/Untitled%202.png](6%20a9208a54bb7649559f2fcafbc940f0e5/Untitled%202.png)

 

 UI오브젝트인 "Canvas/Score", "Canvas/Level", "Canvas/Line" 모두 같은 방법으로 복사-붙여넣기 하여 각각 이름을 S**core2, Level2, Line2**로 바꿔줍니다. 

 앞서 구상한 UI배치도에 따라 UI를 배치해줍니다.

![6%20a9208a54bb7649559f2fcafbc940f0e5/Untitled%203.png](6%20a9208a54bb7649559f2fcafbc940f0e5/Untitled%203.png)

 이후 "Assets/Scripts"에 **Stage2.cs**를 새로 만들어 주고 Stage.cs의 내용을 붙여줍니다.

![6%20a9208a54bb7649559f2fcafbc940f0e5/Untitled%204.png](6%20a9208a54bb7649559f2fcafbc940f0e5/Untitled%204.png)

### 주의사항

- 스크립트의 내용을 복사-붙여넣기 할 경우 스크립트 이름을 잘 변경해주어야 스크립트 오류를 방지할 수 있습니다.

![6%20a9208a54bb7649559f2fcafbc940f0e5/Untitled%205.png](6%20a9208a54bb7649559f2fcafbc940f0e5/Untitled%205.png)

# 2P용 스크립트 수정하기

## 사전설정

 먼저 복사-붙여넣기로 생성한 Stage2 오브젝트에 Stage의 스크립트인 Stage (Script) 를 삭제하고 Stage2.cs 를 새로 적용해줍니다. Remove Component를 이용하여 손쉽게 적용된 스크립트를 삭제할 수 있습니다.

![6%20a9208a54bb7649559f2fcafbc940f0e5/Untitled%206.png](6%20a9208a54bb7649559f2fcafbc940f0e5/Untitled%206.png)

### Source 변경하기

 이후 Source를 Stage2의 Source들로 변경해줍니다. 

 단, Assets>Prefabs의 Tile과 "Canvas/Panel"은 Stage와 Stage2 모두 같은 것을 연결해줍니다.

![6%20a9208a54bb7649559f2fcafbc940f0e5/Untitled%207.png](6%20a9208a54bb7649559f2fcafbc940f0e5/Untitled%207.png)

### 스크립트에 변수 추가하기

 2번째 플레이어는 BG위치와 Preview위치, Tetromino 생성 위치 등을 조정하기 위해 새로운 변수 offset2p를 추가해줍니다. 예시에선 값을 14로 설정하였지만 자신의 UI에 맞게 변경하면됩니다.

```csharp
using UnityEngine;
using UnityEngine.SceneManagement;
using UnityEngine.UI;
public class Stage2 : MonoBehaviour
{

    ...

    [Header("Setting")]
    [Range(4, 40)]
    public int boardWidth = 10;
    //높이 설정
    [Range(5, 20)]
    public int boardHeight = 20;
    //떨어지는 속도
    public float fallCycle = 1.0f;
    //위치 보정
    public float offset_x = 0f;
    public float offset_y = 0f;

    public int offset2p = 14;
```

## 2p 위치 설정하기

두번째 플레이어의 게임 화면은 첫번째 플레이어에 비해 오른쪽으로 offset2p만큼 이동해야합니다. 이 점을 생각하며 Stage2.cs를 수정해야합니다.

![6%20a9208a54bb7649559f2fcafbc940f0e5/Untitled%208.png](6%20a9208a54bb7649559f2fcafbc940f0e5/Untitled%208.png)

### 1. 좌표계 변환하는 경우

 CanMoveTo메서드와 AddToBoard 메서드에서 좌표계 변환시 offset2p를 고려해주어야 합니다. 

```csharp
// 이동 가능한지 체크 후 True or False 반환하는 메서드
    bool CanMoveTo(Transform root)  // tetrominoNode를 매개변수 root로 가져오기
    {
        // tetrominoNode의 자식 타일을 모두 검사
        for (int i = 0; i < root.childCount; ++i)
        {
            var node = root.GetChild(i);
            // 유니티 좌표계에서 테트리스 좌표계로 변환
            int x = Mathf.RoundToInt(node.transform.position.x + halfWidth)-offset2p;
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

```csharp
// 테트로미노를 보드에 추가
    void AddToBoard(Transform root) //tetrominoNode를 매개변수 root로 가져오기
    {
        while (root.childCount > 0)
        {
            var node = root.GetChild(0);

            //유니티 좌표계에서 테트리스 좌표계로 변환
            int x = Mathf.RoundToInt(node.transform.position.x + halfWidth) - offset2p;
            int y = Mathf.RoundToInt(node.transform.position.y + halfHeight - 1);

            //부모노드 : 행 노드(y 위치), 오브젝트 이름 : x 위치
            node.parent = boardNode.Find(y.ToString());
            node.name = x.ToString();
        }
    }
```

### 2. CreateBackground 메서드 수정

 두번째 플레이어의 백그라운드 경우 첫번째 플레이어의 백그라운드에서 offset2p만큼 오른쪽에 그려야합니다. 따라서 CreateBackground의 CreateTile에 offset2p 값을 추가해 배경을 이동시켜줍니다.

```csharp
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
                CreateTile(backgroundNode, new Vector2(x + offset2p, y), color, 0);
            }
        }

        // 좌우 테두리
        color.a = 1.0f;
        for (int y = halfHeight; y > -halfHeight; --y)
        {
            CreateTile(backgroundNode, new Vector2(-halfWidth - 1 + offset2p, y), color, 0);
            CreateTile(backgroundNode, new Vector2(halfWidth + offset2p, y), color, 0);
        }

        // 아래 테두리
        for (int x = -halfWidth - 1; x <= halfWidth; ++x)
        {
            CreateTile(backgroundNode, new Vector2(x + offset2p, -halfHeight), color, 0);
        }
    }
```

### 3. Preview 위치, Tetromino생성위치 수정

 마지막으로 미리보기 위치와 테트로미노 생성위치를 offset2p를 적용하여 이동시켜주면 됩니다.

```csharp
// 나올 예정 테트로미노 보여주기
    void CreatePreview()
    {

        ...

			  // 미리보기 테트로미노 생성 위치 (우측 상단)
        previewNode.position = new Vector2(halfWidth + 5 + offset2p, halfHeight - 1); 
				
				...

        }
    }
    // 테트로미노 생성
    void CreateTetromino()
    {
        ...

				// 테트로미노 생성 위치 (중앙 상단), 값 보정 적용
				tetrominoNode.position = new Vector2(offset_x + offset2p, halfHeight + offset_y);  
  
        ...

    }
```

## 2P 용 키 할당하기

이후 2P용 키를 적용하기 위해 update 메서드의 키 입력 값들을 변경해줍니다.

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

            //각 키에 따라 이동 여부 혹은 회전 여부를 설정해줍니다.
            if (Input.GetKeyDown("left"))
            {
                moveDir.x = -1;

            }
            else if (Input.GetKeyDown("right"))
            {
                moveDir.x = 1;
            }

            if (Input.GetKeyDown("up"))
            {
                isRotate = true;
            }
            else if (Input.GetKeyDown("down"))
            {
                moveDir.y = -1;
            }

            if (Input.GetKeyDown("/"))
            {
                // 테트로미노가 바닥에 닿을 때까지 아래로 이동
                while (MoveTetromino(Vector3.down, false))
                {
                }
            }
					
						...
```

## 보완하기

 실행결과 1P, 2P의 게임 모두 정상작동합니다. 하지만 UI배치가 아직 부족하므로 보완이 필요합니다.

### 보완사항

**1. 1P의 미리보기 위치가 2P 배경과 겹치는 문제**

- 1P의 미리보기는 배경기준 왼쪽 배치하기

**2. 카메라 위치가 2P를 고려하지 않는 문제**

- 카메라의 중심을 오른쪽으로 옮겨 2P도 제대로 나올 수 있게하기

![6%20a9208a54bb7649559f2fcafbc940f0e5/Untitled%209.png](6%20a9208a54bb7649559f2fcafbc940f0e5/Untitled%209.png)

### **메인 카메라 이동**

 offset2p를 14만큼 이동했으므로 절반만큼인 7만큼 MainCamera의 x축 이동을 해줍니다.

![6%20a9208a54bb7649559f2fcafbc940f0e5/Untitled%2010.png](6%20a9208a54bb7649559f2fcafbc940f0e5/Untitled%2010.png)

### **1P 미리보기 위치 이동**

 Stage.cs의 CreatePreview메서드에서 테트로미노 미리보기 위치를 수정해줍니다. 좌측 상단으로 바꾸기 위하여 x값에 -를 추가해줍니다.

```csharp
// 테트로미노 미리보기 기능
    void CreatePreview()
    {

        ...

        // 미리보기 테트로미노 생성 위치 (좌측 상단)
        previewNode.position = new Vector2(-(halfWidth + 5), halfHeight - 1);

        ...
     
    }
```

 실행결과 구상한 UI와 같이 잘 실행되는것을 확인할 수 있습니다.

![6%20a9208a54bb7649559f2fcafbc940f0e5/Untitled%2011.png](6%20a9208a54bb7649559f2fcafbc940f0e5/Untitled%2011.png)

# 2인용 게임 완성하기

## 레벨 디자인 수정하기

 싱글 플레이에선 레벨업이 되면 자신의 테트로미노의 속도를 높여 게임을 어렵게 만들었습니다. 이번엔 2P 대전 게임이므로 레벨업이 되면 자신의 테트로미노의 속도가 아닌 **상대편의 테트로미노의 속도를 높일 수 있게** 해보겠습니다.

다른 스크립트의 변수를 활용하기 위하여 Stage.cs와 Stage2.cs의 `public float fallCycle` 을 `public static float fallCycle`로 변경해 줍니다.

 

### Static

- 클래스에 속해 있는 변수이며, 특정 클래스의 객체에 상관없이 같은 값을 유지함. 즉 다른 스크립트에서 손쉽게 접근하여 수정하거나 읽을 수 있습니다.

```csharp
using UnityEngine;
using UnityEngine.SceneManagement;
using UnityEngine.UI;
public class Stage : MonoBehaviour
{
		...

    //떨어지는 속도
    public static float fallCycle = 1.0f;

		...
```

 그 후 (스크립트이름).(변수이름) 으로 활용할 수 있습니다. Stage.cs에선 `Stage2.fallCycle`로, Stage2.cs에선 `Stage.fallCycle`로 상대방의 속도를 조절할 수 있습니다.

```csharp
// 보드에 완성된 행이 있으면 삭제
    void CheckBoardColumn()
    {

        ...

        // 완성된 행이 있을경우 남은라인 감소
        if (linecount != 0)
        {
            lineVal -= linecount;
            // 레벨업까지 필요 라인 도달경우 (최대 레벨 10으로 한정)
            if (lineVal <= 0 && levelVal <= 10)
            {
                levelVal += 1;  // 레벨증가
                lineVal = levelVal * 2 + lineVal;   // 남은 라인 갱신
                Stage2.fallCycle = 0.1f * (10 - levelVal); // 속도 증가
            }
            level.text = "" + levelVal;
            line.text = "" + lineVal;
        }
```

## 게임오버 조건 수정

 지금까지 2P 추가 이후 게임오버 조건을 수정하지 않아서 두 플레이어 중 한 명이라도 게임 오버 시 전체 게임이 끝나게 됩니다.

 이를 두 플레이어 모두 게임오버 되었을 시 게임이 끝나도록 하고, 두 플레이어 중 점수가 높은 플레이어가 승리했다는 텍스트를 띄워보겠습니다.

### score변수 변경

 먼저 결과 텍스트를 출력하기 위해 Stage.cs에 `public Text result` 를 이용합니다. 그 후 두 플레이어의 점수를 비교하기 위하여 Stage.cs와 Stage2.cs의 `private int scoreVal`을 `public static int scoreVal`로 변경해 줍니다. 그리고 게임오버 여부를 확인할 새로운 변수 `public static int gameOn`을 만들어줍니다. 마지막으로 Start()시 gameOn = true 로 설정해줍니다.

### 주의사항

- 주의할점은 게임오버 관련 시스템은 Stage.cs에서만 관리하므로 public Text result는 Stage.cs에만 추가해 주어야 한다는 것입니다.

```csharp
using UnityEngine;
using UnityEngine.SceneManagement;
using UnityEngine.UI;
public class Stage : MonoBehaviour
{
		//필요 소스 불러오기
    [Header("Source")]
    
		...
    
		public Text result;

    ...

    // UI 관련 변수
    public static int scoreVal = 0;

		...

		public static bool gameOn = true;

		private void Start()
    {
				gameOn = true;
				...
```

### gameOn 변수

**gameOn = false** :  게임 오버 상태

**gameOn = true**  :  게임 실행 상태

에디터로 돌아와서 "Canvas/Panel/Label" 을 Text result에 연결해줍니다.

![6%20a9208a54bb7649559f2fcafbc940f0e5/Untitled%2012.png](6%20a9208a54bb7649559f2fcafbc940f0e5/Untitled%2012.png)

### 결과 출력하기

게임오버시 결과 출력 또한 Stage.cs에서만 관리하므로 Stage.cs만 수정해주면 됩니다.

게임오버시 Stage와 Stage2의 scoreVal값을 비교하여 승리자를 result에 Text로 출력해줍니다.

```csharp
void Update()   // 매 프레임마다 실행
    {
        // 게임오버 처리 (둘 다 게임 끝났을 경우)
        if (gameOn==false&&Stage2.gameOn==false)
        {
            if(scoreVal > Stage2.scoreVal)
                result.text = "1P Win";
            else
                result.text = "2P Win";

            gameoverPanel.SetActive(true);
            if (Input.GetKeyDown("r"))
            {
                SceneManager.LoadScene(0);
            }
        }
        // 게임 처리
        else
        {

						...
```

### 최종결과

 실행 결과 게임오버 텍스트가 잘 나오는 것을 확인할 수 있습니다. 예시에선 비길 경우는 따로 설정해주지 않았지만 비길 경우도 따로 텍스트 설정을 해줄 수 있습니다.

![6%20a9208a54bb7649559f2fcafbc940f0e5/Untitled%2013.png](6%20a9208a54bb7649559f2fcafbc940f0e5/Untitled%2013.png)

# 기타 활용방안 생각해보기

 예시에선 테트리스 만들기를 해보고 새로운 기능들을 추가해보았습니다. 지금까지 배운 내용을 바탕으로 테트리스 게임에 새로운 기능을 더 추가할 수도 있고 새로운 게임을 만들어 보실 수도 있습니다. 각자 자신의 아이디어를 내보고 적용해봅시다.

 다음은 활용방안 예시입니다.

- 블럭모양 바꾸기
- 같은 색갈끼리 맞추었을때 없어지는 타일 만들기
- 사용할 수 있는 아이템 추가하기
- 이펙트 추가하여 이쁘게 만들기
- 건들수 없는 블럭 만들어서 난이도올리기
- 도트 게임 만들기 (eg 갤러그)
- 떨어질 예상위치 보이게 하기
- 새로운 규칙의 퍼즐 게임 만들기
- 슈팅게임 만들기
- 리듬게임 만들기
- ...

## 현재까지 작업결과입니다.

[테트리스 만들기 6](https://drive.google.com/file/d/1_yWrWsIucQlQ80ZfEuDT-IhK1MEVJAaj/view?usp=sharing)