
 [목록으로 돌아가기](L1.md)
 # 테트리스 만들기 1

## 수업내용

- 수업 정보
- 기초 설정과 준비
    - 게임 생성하기
    - 필요 리소스 다운하기
    - 메인 카메라 설정하기
    - 타일 오브젝트 만들기
- 타일 관리 스크립트 작성하기
    - 스크립트 작성 시작하기
    - 오브젝트에 스크립트 적용하기
    - 프리팹 만들기
- 게임 관리 스크립트 작성하기
    - 씬 관리하기
    - Stage 스크립트 생성하고 적용하기
    - 에디터 연동 값 설정하기
    - 좌표계 설정하기

# 수업정보

수업자료 참고 : DoggyHouse 블로그, c#프로그래밍 교재, 

수업 소스 출저 : kenny's source

# **기초 설정과 준비**

## **게임 생성하기**

템플릿 : 2D

버젼 : 19.4.2f

![1%20598b2c3599eb40d7a8ec71da15890ac5/Untitled.png](1%20598b2c3599eb40d7a8ec71da15890ac5/Untitled.png)  
  
## 폴더 생성하기  

Assets창>오른쪽 마우스클릭>Create-Folder 

Images, Scenes, Scripts, Prefabs 폴더를 생성해줍니다.

폴더를 사용하면 리소스를 분할하여 관리하기 편합니다.

![1%20598b2c3599eb40d7a8ec71da15890ac5/1.png](1%20598b2c3599eb40d7a8ec71da15890ac5/1.png)  

## **필요 리소스 다운하기**

[Tile.png](https://drive.google.com/file/d/1CgecNHTuf6lFoEkdPCUQHYUrsmzAaPLS/view?usp=sharing)

 사용할 리소스 불러오기 Assets > Images에 (Tile.png) 드래그 앤 드롭합니다. 유니티에선 드래그앤드롭으로 손쉽게 파일을 불러오고 내보낼 수 있습니다.

![1%20598b2c3599eb40d7a8ec71da15890ac5/Untitled%201.png](1%20598b2c3599eb40d7a8ec71da15890ac5/Untitled%201.png)

속성변경 Pixels Per Unit : **256** 으로 설정해줍니다. 

![1%20598b2c3599eb40d7a8ec71da15890ac5/Untitled%202.png](1%20598b2c3599eb40d7a8ec71da15890ac5/Untitled%202.png)

## **메인 카메라 설정하기**

### 카메라설정값

 **size** =12 , 원하는 배경 색, Position Z에 주의합니다.

### 주의사항

- 카메라 설정시 position Z가 중요합니다.

→ 카메라가 오브젝트보다 앞에 있으면(z값이 크면) 오브젝트가 게임 화면에 나타나지 않을 수 있기 때문입니다.

![1%20598b2c3599eb40d7a8ec71da15890ac5/Untitled%203.png](1%20598b2c3599eb40d7a8ec71da15890ac5/Untitled%203.png)



## **타일 오브젝트 만들기**

Hierarchy창으로 드래그앤드롭을 이용하여 Tile 오브젝트를 만들어 줍니다. 이렇게 이미지를 드래그앤드롭하면 Sprite가 Tile인 빈 오브젝트가 생성됩니다.

![1%20598b2c3599eb40d7a8ec71da15890ac5/Untitled%204.png](1%20598b2c3599eb40d7a8ec71da15890ac5/Untitled%204.png)

# 타일 관리 스크립트 작성하기

## **스크립트 작성 시작하기**

"Assets/Scripts" 에서 Create > c# Script로 스크립트를 생성한 후 **Tile.cs**로 저장합니다.

![1%20598b2c3599eb40d7a8ec71da15890ac5/Untitled%205.png](1%20598b2c3599eb40d7a8ec71da15890ac5/Untitled%205.png)

```csharp
using UnityEngine;

public class Tile : MonoBehaviour
{
	private void Awake()
    {
        spriteRenderer = GetComponent<SpriteRenderer>();

        if (spriteRenderer == null)
        {
            Debug.LogError("You need to SpriteRenderer for Block");
        }
    }
    SpriteRenderer spriteRenderer;

    public Color color
    {
        set
        {
            spriteRenderer.color = value;
        }

        get
        {
            return spriteRenderer.color;
        }
    }

    public int sortingOrder
    {
        set
        {
            spriteRenderer.sortingOrder = value;
        }

        get
        {
            return spriteRenderer.sortingOrder;
        }
    }
}
```

### Awake vs Start vs Update

**Awake** 

- 오브젝트가 생성된 직후 1번만 실행합니다.
- 인스펙터창에서 스크립트요소를 비활성화 해도 실행이 됩니다.
- 스크랩트와 초기화 사이의 모든 레퍼런스 설정에 이용됩니다.

**Start** 

- 게임이 시작되고 첫 번째 프레임 업데이트 이전에 1번만 실행합니다.
- Awake다음으로 첫 업데이트 직전에 호출되지만, 스크립트 요소가 활성화 상태여야 합니다.

**Update** 

- 오브젝트가 준비가 된 후 매 프레임마다 반복 실행합니다.

### Debug.LogError

- SpriteRenderer가 없을경우 오류 상황을 출력합니다.

### Set vs Get

**Set** 

- 멤버변수에 값을 할당합니다.

**Get** 

- 멤버변수에 값을 반환합니다.

외부의 값을 사용하기 위해 `value`키워드를 사용합니다. `val`을 이용하면 명시적인 타입선언 대신 암시적으로 타입변환하여 사용할 수 있습니다.

### 사용 클래스

**spriteRenderer 2D** 

- 그래픽의 스프라이트를 위한 클래스입니다.

**sortingOrder** 

- 스프라이트 표시 순서를 결정하기 위한 속성입니다.

**Color** 

- 스프라이트의 색상을 지정합니다.

 

### 주의사항

- public 객체를 통해 나중에 다른 코드에서 Tile의 spriteRenderer 및 sortingOrder을 활용할 수 있도록 사전 설정을 해둡니다.

## **오브젝트에 스크립트 적용하기**

스크립트 파일을 Hierarchy/Tile 오브젝트 에 드래그 앤 드롭하여 적용해줍니다. 이렇게 적용한 스크립트는 오브젝트의 Inspector창에서 따로 관리할 수 있습니다.

![1%20598b2c3599eb40d7a8ec71da15890ac5/Untitled%206.png](1%20598b2c3599eb40d7a8ec71da15890ac5/Untitled%206.png)

## **프리팹 만들기**

Tile의 설정은 끝났으므로 Hierarchy/Tile 오브젝트 를 "Assets/Prefabs" 폴더로 드래그 앤 드롭 후 Tile오브젝트 삭제해줍니다. Tile오브젝트를 삭제하는 이유는 스크립트에서 Prefab 파일을 불러와 관리할 예정이므로 게임시작전 Tile오브젝트가 존재할 필요가 없기때문입니다.

![1%20598b2c3599eb40d7a8ec71da15890ac5/Untitled%207.png](1%20598b2c3599eb40d7a8ec71da15890ac5/Untitled%207.png)

### Prefab

- 여러 컴포넌트로 이미 구성이 완성된 재사용 가능한 게임 오브젝트입니다.
- 하나의 게임 오브젝트를 여러번 사용해야 할 경우 프리팹을 사용하면 여러곳에 손쉽게 적용할 수 있고 수정할 수 있는 장점이 있습니다.

# 게임 관리 스크립트 작성 시작하기

## Scene **관리하기**

- Hierarchy에 새로만들기 > Create Empty 를 이용하여 **Stage, Board, BG, Tetromino** 이름의 오브젝트를 만들어 줍니다.
- F2번 단축키(오브젝트명 변경), Ctrl + D (오브젝트 복사,붙여넣기)를 이용하면 효과적입니다.

![1%20598b2c3599eb40d7a8ec71da15890ac5/Untitled%208.png](1%20598b2c3599eb40d7a8ec71da15890ac5/Untitled%208.png)

### 오브젝트 구성요소

**Board** 

- 화면에 배치된 테트리스 블록을 관리하기 위한 오브젝트입니다.
- Tetromino가 바닥에 닿으면 Board 오브젝트로 상속이 바뀝니다.

**BG** 

- background 타일을 관리하기 위한 오브젝트입니다.

**Tetromino** 

- 테트리스 게임중에 아래로 이동하고 있는 블록들을 관리하기 위한 오브젝트입니다.
- 이동이 종료후, Board 오브젝트에 상속됩니다.

**Stage** 

- 위 세가지 오브젝트를 묶어서 관리하기 위한 오브젝트입니다.

## **Stage 스크립트 생성 후 적용하기**

위의 스크립트 생성, 적용 방법을 이용하여 Stage오브젝트에 **Stage.cs**스크립트 적용시켜 줍니다.

![1%20598b2c3599eb40d7a8ec71da15890ac5/Untitled%209.png](1%20598b2c3599eb40d7a8ec71da15890ac5/Untitled%209.png)

## **에디터 연동 값 설정하기**

유니티 에디터 기능을 이용하여 스크립트 밖에서 스크립트 값 조정과 오브젝트 연동을 할 수 있습니다.

### 유니티 에디터

- Property 값들을 설정할 수 있는 패널을 뜻합니다.
- 기본적으로 유니티 내 게임 오브젝트에 스크립트를 부착하고 그 안에 클래스들의 변수들이 public으로 설정되어 있으면 하나의 인스펙터로 구분, 관리할 수 있습니다.

### Stage스크립트 작성하기

```csharp
using UnityEngine;
public class Stage : MonoBehaviour
{
    //필요 소스 불러오기
    [Header("Source")]
    public GameObject tilePrefab;
    public Transform backgroundNode;
    public Transform boardNode;
    public Transform tetrominoNode;

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
}
```

### Transform

- 게임 오브젝트가 가지는 기본 컴포넌트입니다.
- 위치, 회전, 크기 정보를 담고 있으며, 부모관계 설정, 관리할 수 있습니다.

### GameObject

- Prefab 오브젝트를 불러와서 관리 가능합니다.

### 유니티 에디터 관련 코드

**[Header("Title")]**

- 그룹 이름을 지어 구분짓기를 가능케해줍니다.

→ 유니티 에디터 필요 변수들이 많아질 경우 관리하기 편리합니다.

**[Range(a,b)]** 

- 사용자에게 입력받을 값의 범위를 정해주어 오류를 방지하는 기능을 합니다.

위의 코드를 이용하여 Stage오브젝트에서 Stage 스크립트의 값들을 손쉽게 관리 가능합니다.

![1%20598b2c3599eb40d7a8ec71da15890ac5/Untitled%2010.png](1%20598b2c3599eb40d7a8ec71da15890ac5/Untitled%2010.png)

### Source 연결하기

이제 위의 Source에 필요 오브젝트와 Prefab을 드래그앤드롭으로 연결합니다.

**Tile Prefab** : Asstes / Prefabs / Tile

**backgroundNode** : Stage / BG

**boardBode** : Stage / Board

**tetrominoNode** : Stage / Tetromino

![1%20598b2c3599eb40d7a8ec71da15890ac5/Untitled%2011.png](1%20598b2c3599eb40d7a8ec71da15890ac5/Untitled%2011.png)

다음과 같이 Source에 연결을 모두 완료하면 됩니다. 연결을 완료했다면 아래의 그림과같이 Stage(Script)에 원하는 노드들의 이름을 볼 수 있습니다.

![1%20598b2c3599eb40d7a8ec71da15890ac5/Untitled%2012.png](1%20598b2c3599eb40d7a8ec71da15890ac5/Untitled%2012.png)

## **좌표계 설정하기**

 유니티의 좌표계는 기본적으로 화면 중심을 기준으로 0, 0 이며 오른쪽, 위쪽으로 +값, 왼쪽, 아래쪽으로는 -값을 가집니다.

 이러한 유니티 좌표계를 기반으로 게임을 만들 수 있지만, 나중에 값을 관리하기 어렵고 헷갈릴 수 있음으로 테트리스에 알맞은 좌표계로 변환을 한 뒤 게임을 만들어 보겠습니다.

### 테트리스 좌표계 구상도

![1%20598b2c3599eb40d7a8ec71da15890ac5/Untitled%2013.png](1%20598b2c3599eb40d7a8ec71da15890ac5/Untitled%2013.png)

이렇게 원점을 이동하기 위해 게임에 사용할 보드의 너비(width)값과 높이(Height)값을 이용하여 변환해보겠습니다.

![1%20598b2c3599eb40d7a8ec71da15890ac5/Untitled%2014.png](1%20598b2c3599eb40d7a8ec71da15890ac5/Untitled%2014.png)

### 주의사항

- 이러한 나눗셈 등의 수학적 연산을 할 경우 소수를 정수로 변환할 때 원하는 값이 나오지 않을 경우 고려해주어야 합니다.
- `(int)` 이용한 정수 변환이나 `Mathf.RoundToInt`를 이용하여 가장 가까운 정수로 변환하는 방법을 이용해야 합니다.
- 작은 오차는 오프셋 값을 이용하여 원하는 값으로 조정할 수 있습니다.

## 현재까지 작업결과입니다.

[테트리스 만들기 1](https://drive.google.com/file/d/1R38milx3uzAU6aMjO7IhrhA_G5qmOs9-/view?usp=sharing)


 [목록으로 돌아가기](L1.md)
