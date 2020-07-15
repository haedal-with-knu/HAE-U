# 테트리스 만들기 1

---

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
- 게임 관리 스크립트 작성 시작하기
    - 씬 관리하기
    - Stage 스크립트 만들고 오브젝트에 적용하기
    - c# 스크립트 : 에디터 연동값 설정
    - c# 스크립트 : 좌표계 설정

---

## 수업정보

수업자료 참고 : DoggyHouse 블로그, c#프로그래밍 교재, 

수업 소스 출저 : kenny's source

---

## **기초 설정과 준비**

### **게임 생성하기**

템플릿 : 2D

버젼 : 19.4.2f

![1%2075b532fac3d84ef694ffddc9ab2502bf/Untitled.png](1%2075b532fac3d84ef694ffddc9ab2502bf/Untitled.png)

### **필요 리소스 다운하기**

[Tile.png](https://drive.google.com/file/d/1CgecNHTuf6lFoEkdPCUQHYUrsmzAaPLS/view?usp=sharing)

사용할 리소스 불러오기 Assets > Images 에 (Tile.png) 드래그

![1%2075b532fac3d84ef694ffddc9ab2502bf/Untitled%201.png](1%2075b532fac3d84ef694ffddc9ab2502bf/Untitled%201.png)

속성변경 Pixels Per Unit : 256

![1%2075b532fac3d84ef694ffddc9ab2502bf/Untitled%202.png](1%2075b532fac3d84ef694ffddc9ab2502bf/Untitled%202.png)

### **메인 카메라 설정하기**

size : 12

![1%2075b532fac3d84ef694ffddc9ab2502bf/Untitled%203.png](1%2075b532fac3d84ef694ffddc9ab2502bf/Untitled%203.png)

### **타일 오브젝트 만들기**

드래그앤드롭 이용하여 Tile 오브젝트 만들기

![1%2075b532fac3d84ef694ffddc9ab2502bf/Untitled%204.png](1%2075b532fac3d84ef694ffddc9ab2502bf/Untitled%204.png)

---

## 타일 관리 스크립트 작성하기

### **스크립트 작성 시작하기**

Assets > Scripts 에서 Create > c# Script로 스크립트를 생성한 후 Tile.cs로 이름을 정해줍니다.

![1%2075b532fac3d84ef694ffddc9ab2502bf/Untitled%205.png](1%2075b532fac3d84ef694ffddc9ab2502bf/Untitled%205.png)

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

Awake

해당 오브젝트가 로딩된 후 가장 처음으로 불리는 것.

Tip 

Awake : 오브젝트가 생성된 직후

Start : 게임이 시작되고 첫 번째 프레임 업데이트 이전

Update : 오브젝트가 준비가 된 후 매 프레임마다

Debug.LogError을 이용하여 SpriteRenderer가 없을경우 오류 상황을 출력

tip : Set Get method

Set : 멤버변수에 값을 할당

Get : 멤버변수에 값을 반환

외부의 값을 사용하기 위해 `value`키워드를 사용합니다.

사용 클래스

**spriteRenderer** 2D 그래픽의 스프라이트를 위한 클래스 

**sortingOrder** 스프라이트 표시 순서를 결정하기 위한 속성.

**Color** 스프라이트의 색상을 지정.

이러한 public 객체를 만들어 두어 나중에 다른 코드에서 Tile의spriteRenderer 및 sortingOrder을 활용할 수 있도록 사전설정 해둠.

### **오브젝트에 스크립트 적용하기**

스크립트 파일을 Hierarchy > Tile오브젝트 에 드래그앤드롭하기

![1%2075b532fac3d84ef694ffddc9ab2502bf/Untitled%206.png](1%2075b532fac3d84ef694ffddc9ab2502bf/Untitled%206.png)

### **프리팹 만들기**

Tile의 설정은 끝났으므로 Hierarchy > Tile오브젝트 를 Assets > Prefabs 폴더로 드래그 앤 드롭 후 Tile오브젝트 삭제해주기

![1%2075b532fac3d84ef694ffddc9ab2502bf/Untitled%207.png](1%2075b532fac3d84ef694ffddc9ab2502bf/Untitled%207.png)

---

## 게임 관리 스크립트 작성 시작하기

### **씬 관리하기**

Hierarchy에 새로만들기 → Create Empty를 이용하여 Stage, Board, BG, Tetromino를 만들어줍니다.

![1%2075b532fac3d84ef694ffddc9ab2502bf/Untitled%208.png](1%2075b532fac3d84ef694ffddc9ab2502bf/Untitled%208.png)

Board : 화면에 배치된 블록 관리. Tetromino가 바닥에 닿으면 Board로 바뀜.

BG : background 타일

Tetromino : 테트리스에서 이동하고 있는 블록

Stage : 위 세가지 오브젝트를 묶어서 관리위

### **Stage 스크립트 만들고 오브젝트에 적용하기**

위의 스크립트 생성, 적용 방법을 이용하여 Stage오브젝트에 Stage.cs스크립트 적용시키기.

![1%2075b532fac3d84ef694ffddc9ab2502bf/Untitled%209.png](1%2075b532fac3d84ef694ffddc9ab2502bf/Untitled%209.png)

### c#스크립트 : **에디터 연동값 설정**

유니티 에디터라는 기능을 이용하여 스크립트 밖에서 스크립트 값 조정 & 오브젝트 연동 가능.

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

[Header("Title")]

그룹 이름을 지어 구분짓기 가능.

→ 유니티 에디터 필요 변수들이 많아질 경우 관리하기 편리함

[Range(a,b)] 

사용자에게 입력받을 값의 범위를 정해주어 오류를 방지 가능.

위의 코드를 작성하면 Stage오브젝트에서 Stage 스크립트의 값들을 손쉽게 관리 가능함.

![1%2075b532fac3d84ef694ffddc9ab2502bf/Untitled%2010.png](1%2075b532fac3d84ef694ffddc9ab2502bf/Untitled%2010.png)

이제 위의 Source에 필요 오브젝트와 Preab을 드래그앤 드롭으로 연결합니다.

Tile Prefab : Asstes / Prefabs / Tile

backgroundNode : Stage / BG

boardBode : Stage / Board

tetrominoNode : Stage / Tetromino

![1%2075b532fac3d84ef694ffddc9ab2502bf/Untitled%2011.png](1%2075b532fac3d84ef694ffddc9ab2502bf/Untitled%2011.png)

![1%2075b532fac3d84ef694ffddc9ab2502bf/Untitled%2012.png](1%2075b532fac3d84ef694ffddc9ab2502bf/Untitled%2012.png)

### c#스크립트 : **좌표계 설정**

유니티의 좌표계는 화면을 중심을 기준으로 0,0 이며 오른쪽, 위쪽으로 +값, 왼쪽, 아래쪽으로는 -값을 가집니다.

 이러한 유니티 좌표계를 기반으로 게임을 만들수 있지만 나중에 값을 관리하기 어렵고 헷갈릴 수 있으므로 테트리스에 알맞은 좌표계로 변환을 한 뒤 게임을 만들어 보겠습니다.

![1%2075b532fac3d84ef694ffddc9ab2502bf/Untitled%2013.png](1%2075b532fac3d84ef694ffddc9ab2502bf/Untitled%2013.png)

이렇게 원점을 이동하기 위해 게임에 사용할 보드의 너비(width)값과 높이(Height)값을 이용하여 변환해보겠습니다.

![1%2075b532fac3d84ef694ffddc9ab2502bf/Untitled%2014.png](1%2075b532fac3d84ef694ffddc9ab2502bf/Untitled%2014.png)

주의 : 이러한 나눗셈 등의 수학적 연산을 할 경우 소수를 정수로 변환할 때 원하는 값이 나오지 않을 경우 고려해주어야함.

→ (int)이용한 정수 변환이나 Mathf.RoundToInt()를 이용하여 가장 가까운 정수로 변환하는 방법을 이용해야합니다.

→또는 오프셋 값을 이용하여 원하는 값으로 조정해 주어야합니다.

---

### 현재까지 작업결과입니다.

[테트리스 만들기 1](https://drive.google.com/file/d/1R38milx3uzAU6aMjO7IhrhA_G5qmOs9-/view?usp=sharing)