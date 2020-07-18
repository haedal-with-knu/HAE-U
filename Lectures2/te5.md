# 테트리스 만들기 5

---

## 수업내용

- UI 시작하기
    - UI 이해하기
    - 전체적인 UI 배치 구상하기
    - UI 사용위한 사전설정하기
- 점수 및 레벨 시스템 추가하기
    - 점수 시스템 관리하기
    - 레벨 시스템 관리하기
- 테트로미노 미리보기 기능 구현
    - 사전설정
    - 미리보기 기능 구상하기
    - 미리보기 메서드 작성하기

---

## UI시작하기

 전 시간에 게임오버 화면을 만들어보았습니다. 게임오버 화면을 위한 패널과 텍스트 모두 UI기능을 이용한 것입니다. 오늘은 이 UI (UserInterface)에 대해 알아보고 새로운 UI를 추가해보도록 하겠습니다.

### **UI 이해하기**

### 전체적인 UI 배치 구상하기

먼저 필요한 UI 가 어떤것들이 있는지 생각해봅시다.

![5%20c00fa454c85e4281b3ee3ec885c03928/Untitled.png](5%20c00fa454c85e4281b3ee3ec885c03928/Untitled.png)

출저 : ClassicTetrisWorldChampionship 

 일반적으로 테트리스 게임 화면은 메인 게임 화면뿐 아니라 점수, 현재 레벨(단계), 레벨업을 위한 필요 클리어 줄 개수, 그리고 나올 예정인 테트로미노를 보여주는 화면으로 구성되어 있습니다.

 이러한 기본적인 요소들을 추가해보고 스크립트에 코드를 작성하기 전에 전체적인 UI배치를 대략적으로 구상해보아야합니다. 저는 간단하게 아래와 같이 구상해보았습니다. UI 위치와 구성 방법 등은 본인이 원하는대로 구상해보시기 바랍니다.

![5%20c00fa454c85e4281b3ee3ec885c03928/Untitled%201.png](5%20c00fa454c85e4281b3ee3ec885c03928/Untitled%201.png)

### UI 사용위한 사전설정하기

먼저 Canvas를 제대로 사용하기 위하여 저번에 만들어두었던 GameOver용 Panel을 꺼두겠습니다. 아래 그림처럼 이름 좌측의 체크를 해제하시면 됩니다.

![5%20c00fa454c85e4281b3ee3ec885c03928/Untitled%202.png](5%20c00fa454c85e4281b3ee3ec885c03928/Untitled%202.png)

이제 Canvas에 UI>Text 로 Text파일을 3개 만들어줍니다. 각 오브젝트 이름을 Score, Level, Line으로 설정해줍니다. 각각 점수표시, 레벨표시, 남은 라인표시를 담당할 오브젝트입니다.

![5%20c00fa454c85e4281b3ee3ec885c03928/Untitled%203.png](5%20c00fa454c85e4281b3ee3ec885c03928/Untitled%203.png)

![5%20c00fa454c85e4281b3ee3ec885c03928/Untitled%204.png](5%20c00fa454c85e4281b3ee3ec885c03928/Untitled%204.png)

 앞서 생각해둔 구상도에 따라서 원하는 위치에 텍스트를 배치해줍니다. 

![5%20c00fa454c85e4281b3ee3ec885c03928/Untitled%205.png](5%20c00fa454c85e4281b3ee3ec885c03928/Untitled%205.png)

위에서 만든 Text 오브젝트들을 불러올 수 있도록 유니티에디터를 수정해 줍니다. 가장 상단에 using UnityEngine.UI 코들드를 이용하여 Text 기능을 사용할 수 있습니다.

```csharp
using UnityEngine;
using UnityEngine.SceneManagement;
using UnityEngine.UI;
public class Stage : MonoBehaviour
{
    //필요 소스 불러오기
    [Header("Source")]
    public GameObject tilePrefab;
    public Transform backgroundNode;
    public Transform boardNode;
    public Transform tetrominoNode;

    public GameObject gameoverPanel;
    public Text score;
    public Text level;
    public Text line;

		...
```

 에디터로 돌아와서 "Canvas/Score, Level, Line" 을 모두 연결해줍니다.

![5%20c00fa454c85e4281b3ee3ec885c03928/Untitled%206.png](5%20c00fa454c85e4281b3ee3ec885c03928/Untitled%206.png)

 

 앞으로 UI 에서 사용할 변수 `scoreVal`, `levelVal`, `lineVal`를 선언해줍니다. 각각 전체 점수, 레벨, 남은 라인 개수를 저장하는 정수값을 의미합니다.

 그리고 게임을 시작했을 경우 text가 화면에 표시되도록 UI기능을 이용해 스크립트를 작성해보겠습니다.

```csharp
using UnityEngine;
using UnityEngine.SceneManagement;
using UnityEngine.UI;
public class Stage : MonoBehaviour
{
    ...

    // UI 관련 변수
    private int scoreVal = 0;
    private int levelVal = 1;
    private int lineVal;

		private void Start()
    {
				// 게임 시작시 text 설정
        lineVal = levelVal * 2;   // 임시 레벨 디자인
        score.text = "" + scoreVal;
        level.text = "" + levelVal;
        line.text = "" + lineVal;

				...
```

 여기까지 잘 따라오셨다면 게임을 실행하였을때 간단한 UI를 확인할 수 있습니다.

![5%20c00fa454c85e4281b3ee3ec885c03928/Untitled%207.png](5%20c00fa454c85e4281b3ee3ec885c03928/Untitled%207.png)

---

## 점수 및 레벨 시스템 추가하기

### 점수 시스템 관리하기

 테트리스는 한꺼번에 많은 행을 동시에 없앨경우 더 큰 점수를 얻게되는 시스템이 일반적입니다. 점수기능을 추가하기 위해 `CheckBoardColumn` 메서드를 수정해보겠습니다. `linecount`라는 변수를 사용하여 한번에 없어진 행의 개수를 셀 수 있게 하였습니다.

```csharp
// 보드에 완성된 행이 있으면 삭제
    void CheckBoardColumn()
    {
        bool isCleared = false;

				//한번에 사라진 행 개수 확인용
        int linecount = 0;

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
	              linecount++; // 완성된 행 하나당 linecount 증가
            }
        }
        // 완성된 행이 있을경우 점수증가
        if (linecount != 0)
        {
            scoreVal += linecount * linecount * 100;
            score.text = "" + scoreVal;
        }

        ...        
```

 예시에선 점수 계산식을 scoreVal = *linecount^2 * 100*  으로 하여 계산하였지만 원하는 점수 계산식을 만들어 사용하시는 방법도 있습니다.

 

 현재까지 작업의 테스트 결과 점수가 잘 반영되는지 확인할 수 있습니다.

![5%20c00fa454c85e4281b3ee3ec885c03928/Untitled%208.png](5%20c00fa454c85e4281b3ee3ec885c03928/Untitled%208.png)

### 레벨 시스템 관리하기

 위에서 점수증가 코드에 이어서 `CheckBoardColumn` 메서드를 수정해보겠습니다.

```csharp
// 보드에 완성된 행이 있으면 삭제
    void CheckBoardColumn()
    {

        ...

        // 완성된 행이 있을경우 점수증가
        if (linecount != 0)
        {
            scoreVal += linecount * linecount * 100;
            score.text = "" + scoreVal;
        }

        // 완성된 행이 있을경우 남은라인 감소
        if (linecount != 0)
        {
            lineVal -= linecount;
            // 레벨업까지 필요 라인 도달경우 (최대 레벨 10으로 한정)
            if (lineVal <= 0 && levelVal<=10)
            {
                levelVal += 1;  // 레벨증가
                lineVal = levelVal * 2 + lineVal;   // 남은 라인 갱신
                fallCycle = 0.1f*(10-levelVal); // 속도 증가
            }
            level.text = "" + levelVal;
            line.text = "" + lineVal;
        }             
				
				...

```

 `lineVal`를 완성된 line갯수인 `linecount`만큼 감소시켜 남은 라인 개수를 업데이트합니다.

 이때 `lineVal`가 0이하면 레벨업 조건을 만족하므로 `levelVal`를 증가시키고 다음 레벨에 필요한 `lineVal`를 업데이트 해줍니다. 레벨이 증가할수록 게임을 어렵게 하기위하여 테트로미노의 속도인 `fallCycle`값을 조정해주었습니다. 마찬가지로`lineVal`계산식이나 속도 증가식 모두 각자 원하는 식을 이용하여도 좋습니다.

 마지막으로 변경된 값들을 UI에 반영하기 위하여 `level.text` 와 `line.text`를 이용하여 업데이트해줍니다.

 테스트결과, 남은 개수변화와 레벨 변화, 속도 변화를 확인해 볼 수 있습니다.

![5%20c00fa454c85e4281b3ee3ec885c03928/Untitled%209.png](5%20c00fa454c85e4281b3ee3ec885c03928/Untitled%209.png)

## 테트로미노 미리보기 기능 구현

### 사전설정

 먼저 미리보기의 테트로미노를 관리하기 위하여 previewNode를 유니티에디터에 추가합니다. 그 후 미리보기의 테트로미노의 Index값을 저장해두기 위한 indexVal 라는 정수를 선언해줍니다.

```csharp
using UnityEngine;
using UnityEngine.SceneManagement;
using UnityEngine.UI;
public class Stage : MonoBehaviour
{
		//필요 소스 불러오기
    [Header("Source")]
    public GameObject tilePrefab;
    public Transform backgroundNode;
    public Transform boardNode;
    public Transform tetrominoNode;
    public Transform previewNode;

    ...

    private int scoreVal=0;
    private int levelVal=1;
    private int lineVal;

    private int indexVal=-1;

    private void Start()
    {

		    ...

```

에디터로 돌아와서 "Stage/Preview" 를 연결해줍니다.

![5%20c00fa454c85e4281b3ee3ec885c03928/Untitled%2010.png](5%20c00fa454c85e4281b3ee3ec885c03928/Untitled%2010.png)

### 미리보기 기능 구상하기

 미리보기 기능을 만들기 전에 전체적인 작성 순서 및 고려사항을 생각해보겠습니다. 

- 새로운 변수 indexVal를 이용하여 미리보기의 테트로미노가 다음 내려오는 테트로미노에 반영되도록 하여야합니다.
- 새로운 테트로미노가 생성되었을때 이전 미리보기를 삭제한 후 새로 랜덤으로 만들어야합니다.
- 제일 최초의 테트로미노는 이전 미리보기가 없으므로 랜덤으로 생성해주어야 합니다.

제일 최초의 테트로미노 여부는 indexVal의 초기값이 -1임을 이용할 예정입니다.

![5%20c00fa454c85e4281b3ee3ec885c03928/Untitled%2011.png](5%20c00fa454c85e4281b3ee3ec885c03928/Untitled%2011.png)

### 미리보기 메서드 작성하기

 테트로미노 미리보기 기능을 위해 CreatePreview() 메서드를 작성해보겠습니다.

 테트로미노 미리보기 기능을 작성할 경우 생성 전 이미 존재하는 미리보기가 있는지 확인 후 삭제해 주어야합니다. 

 예시 코드에선 테트로미노 미리보기 위치를 halfWidth+5, halfHeight-1 로 두었지만 원하는 위치로 바꾸어도 괜찮습니다.

```csharp
// 테트로미노 미리보기
    void CreatePreview()
    {
        // 이미 있는 미리보기 삭제하기
        foreach (Transform tile in previewNode)
        {
            Destroy(tile.gameObject);
        }
        previewNode.DetachChildren();

        indexVal = Random.Range(0, 7);

        Color32 color = Color.white;

				// 미리보기 테트로미노 생성 위치 (우측 상단)
        previewNode.position = new Vector2(halfWidth + 5, halfHeight - 1);    

        switch (indexVal)
        {
            case 0: // I
                color = new Color32(115, 251, 253, 255);    // 하늘색
                CreateTile(previewNode, new Vector2(-2f, 0.0f), color);
                CreateTile(previewNode, new Vector2(-1f, 0.0f), color);
                CreateTile(previewNode, new Vector2(0f, 0.0f), color);
                CreateTile(previewNode, new Vector2(1f, 0.0f), color);
                break;

            case 1: // J
                color = new Color32(0, 33, 245, 255);    // 파란색
                CreateTile(previewNode, new Vector2(-1f, 0.0f), color);
                CreateTile(previewNode, new Vector2(0f, 0.0f), color);
                CreateTile(previewNode, new Vector2(1f, 0.0f), color);
                CreateTile(previewNode, new Vector2(-1f, 1.0f), color);
                break;

            case 2: // L
                color = new Color32(243, 168, 59, 255);    // 주황색
                CreateTile(previewNode, new Vector2(-1f, 0.0f), color);
                CreateTile(previewNode, new Vector2(0f, 0.0f), color);
                CreateTile(previewNode, new Vector2(1f, 0.0f), color);
                CreateTile(previewNode, new Vector2(1f, 1.0f), color);
                break;

            case 3: // O 
                color = new Color32(255, 253, 84, 255);    // 노란색
                CreateTile(previewNode, new Vector2(0f, 0f), color);
                CreateTile(previewNode, new Vector2(1f, 0f), color);
                CreateTile(previewNode, new Vector2(0f, 1f), color);
                CreateTile(previewNode, new Vector2(1f, 1f), color);
                break;

            case 4: //  S
                color = new Color32(117, 250, 76, 255);    // 녹색
                CreateTile(previewNode, new Vector2(-1f, -1f), color);
                CreateTile(previewNode, new Vector2(0f, -1f), color);
                CreateTile(previewNode, new Vector2(0f, 0f), color);
                CreateTile(previewNode, new Vector2(1f, 0f), color);
                break;

            case 5: //  T
                color = new Color32(155, 47, 246, 255);    // 자주색
                CreateTile(previewNode, new Vector2(-1f, 0f), color);
                CreateTile(previewNode, new Vector2(0f, 0f), color);
                CreateTile(previewNode, new Vector2(1f, 0f), color);
                CreateTile(previewNode, new Vector2(0f, 1f), color);
                break;

            case 6: // Z
                color = new Color32(235, 51, 35, 255);    // 빨간색
                CreateTile(previewNode, new Vector2(-1f, 1f), color);
                CreateTile(previewNode, new Vector2(0f, 1f), color);
                CreateTile(previewNode, new Vector2(0f, 0f), color);
                CreateTile(previewNode, new Vector2(1f, 0f), color);
                break;
        }
    }
```

 

 이제 미리보기 기능을 사용하기위해 indexVal값을 이용하여 CreateTetromino 메서드를 수정해줍니다. indexVal가 -1일 경우 이전 미리보기 값이 없는 상태이므로 Random을 이용하여 index값을 정해줍니다. 미리보기 값이 있는경우 index값을 indexVal로 설정해줍니다.

 마지막으로 CreatePreview를 CreateTetromino메서드 마지막줄에 추가해줍니다.

```csharp
// 테트로미노 생성
    void CreateTetromino()
    {
        //제일 처음에 나오는 테트로미노인경우
        int index;
        if (indexVal == -1)
        {
            index = Random.Range(0, 7); // 랜덤으로 0~6 사이의 값 생성
        }
        else index = indexVal;  // Preview의 값 가져오기

        ...
   
        switch (index)
        {

            ...
            
        }
        CreatePreview();
    }
```

### 현재까지 작업결과입니다.

[테트리스만들기5](https://drive.google.com/file/d/1mkduaSj8OFT4gOPX7P0STiYjuPqxam5a/view?usp=sharing)