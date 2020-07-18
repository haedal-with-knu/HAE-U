# 플랫폼 게임만들기 1

## 수업내용

- 수업 정보
- 기초 설정과 준비
    - 게임 생성하기
    - 필요 리소스 다운하기
    - 스프라이트 관리하기
- 기본 요소 관리하기
    - 오브젝트 생성하기
    - 카메라설정
    - physics2D 설정
    - 플레이어와 블럭 생성하기
- 본격적인 프로그래밍 들어가기
    - c# 스크립트란
    - 플레이어 움직임 코딩하기
    - 플레이어 키 입력받기
    - 유니티 에디터 설정하기
    - 점프 설정 바꾸기
    - 적 구현하기
    - 적과 충돌시 대응하기
    - 부드러운 카메라 무빙 적용하기

## 수업정보

수업자료 참고 : DoggyHouse 블로그, c#프로그래밍 교재, 

수업 소스 출저 : kenny's source

---

## **기초 설정과 준비**

### **게임 생성하기**

템플릿 : 2D

버젼 : 19.4.2f

### **필요 리소스 다운하기**

### 기본 설정 - Sprite 불러오기

![1%202742062629d646bcb65f0d7e4fc79683/Untitled.png](1%202742062629d646bcb65f0d7e4fc79683/Untitled.png)

Drag&Drop으로 쉽게 이미지 파일을 옮길 수 있다.

**Sprite 정보창**

**SpriteMode : Multiple**    이미지 자를지 여부 설정

**SpriteEditor**    세부 sprite 설정용

**FilterMode : Point**     비트이미지 뭉개지지 않게 설정 가능

![1%202742062629d646bcb65f0d7e4fc79683/Untitled%201.png](1%202742062629d646bcb65f0d7e4fc79683/Untitled%201.png)

### **SpriteEditor란**

**Grid By Cell Size** : 각 sprite가 일정한 크기일 경우 이용

**Automatic** : 각 sprite를 원하는 크기로 따로따로 자를 경우 이용

일정한 크기로 자르고 싶으므로 grid by cell size로 **X=96, Y=128**로 크기설정  

![1%202742062629d646bcb65f0d7e4fc79683/Untitled%202.png](1%202742062629d646bcb65f0d7e4fc79683/Untitled%202.png)

하나의 이미지를 손쉽게 잘라서 관리할 수 있다.

> 주의 :  spriteEditor 실행 안될시 PacakageManager이용하기

![1%202742062629d646bcb65f0d7e4fc79683/Untitled%203.png](1%202742062629d646bcb65f0d7e4fc79683/Untitled%203.png)

## 기본요소 관리하기

### 오브젝트만들기

![1%202742062629d646bcb65f0d7e4fc79683/Untitled%204.png](1%202742062629d646bcb65f0d7e4fc79683/Untitled%204.png)

원하는 이미지 파일을 Scene에 Drag&Drop으로 손쉽게 오브젝트를 만들 수 있다.

### 카메라 설정

카메라설정 : size =4 

카메라 설정시 position Z가 중요 → 카메라가 오브젝트보다 앞에있으면(z값이 크면) 오브젝트가 게임 화면에 나타나지 않을 수 있다.

![1%202742062629d646bcb65f0d7e4fc79683/Untitled%205.png](1%202742062629d646bcb65f0d7e4fc79683/Untitled%205.png)

### Physics 2D 설정

file → build settings → player settings → physics 2D →Gravity Y = -20

![1%202742062629d646bcb65f0d7e4fc79683/Untitled%206.png](1%202742062629d646bcb65f0d7e4fc79683/Untitled%206.png)

![1%202742062629d646bcb65f0d7e4fc79683/Untitled%207.png](1%202742062629d646bcb65f0d7e4fc79683/Untitled%207.png)

### Player, Block 만들기

**Player**

1. RigidBody2D 설정 → Freeze Rotation z해주기
2. BoxCollider 2D 설정 → Edit Collider로 충돌범위 조정

**Block**

1. RigidBody2D 설정 → Freeze Rotation, Position 모두 해주기
2. BoxCollider 2D 설정 → Edit Collider로 충돌범위 조정
3. 태그붙이기
4. 앞으로 자주 사용할 것이므로 prefabs설정하기

태그붙이는 과정

![1%202742062629d646bcb65f0d7e4fc79683/Untitled%208.png](1%202742062629d646bcb65f0d7e4fc79683/Untitled%208.png)

![1%202742062629d646bcb65f0d7e4fc79683/Untitled%209.png](1%202742062629d646bcb65f0d7e4fc79683/Untitled%209.png)

![1%202742062629d646bcb65f0d7e4fc79683/Untitled%2010.png](1%202742062629d646bcb65f0d7e4fc79683/Untitled%2010.png)

## c# 스크립트 다루기

### **c#스크립트란?**

c#스크립트란 c++의 강력함 + VB의 편리함 + JAVA의 독립적 플랫폼 장점들을 모두 모은 유니티에서 사용하는 언어입니다.UNITY의 c#스크립트의 기본적인 구성을 알아보자.

**기본적인 유니티 스크립트 구성**

![1%202742062629d646bcb65f0d7e4fc79683/Untitled%2011.png](1%202742062629d646bcb65f0d7e4fc79683/Untitled%2011.png)

스크립트 생성시  처음 볼 수 있는 화면.   필요한 코드를 제외하고 지우고 시작하자

위의 코드를 살펴보면, 첫줄의 `using` 은 다른 lib의 코드를 import하는 기능으로 ~, `public class` 는 자바의 객체 역할을, 마지막으로 `void Start()` 는 자바의 메소드를 의미합니다.

스크립트를 실행하면 Start(실행 시)와 Update(실행 중)메소드 안에 작성한 스크립트 코드가 실행됩니다.

![https://user-images.githubusercontent.com/48755297/87010803-11a57280-c202-11ea-8c04-b529f2e85ef1.PNG](https://user-images.githubusercontent.com/48755297/87010803-11a57280-c202-11ea-8c04-b529f2e85ef1.PNG)

### 플레이어 움직임 코딩하기

Assets에 Scripts폴더 추가 후 PlayerMovement c#스크립트를 만들어줍니다.

![1%202742062629d646bcb65f0d7e4fc79683/Untitled%2012.png](1%202742062629d646bcb65f0d7e4fc79683/Untitled%2012.png)

```csharp
using UnityEngine;

public class PlayerMovement : MonoBehaviour
{
    public float movePower = 1f;
    public float jumpPower = 1f;

    Rigidbody2D rigid;

    Vector3 movement;
    bool isJumping = false;

    void Start()
    {
        rigid = gameObject.GetComponent<Rigidbody2D>();
    }
}
```

```csharp
using UnityEngine;

public class PlayerMovement : MonoBehaviour
{
    public float movePower = 1f;
    public float jumpPower = 1f;

    Rigidbody2D rigid;

    Vector3 movement;
    bool isJumping = false;

    void Start()
    {
        rigid = gameObject.GetComponent<Rigidbody2D>();
    }
}
```

`GetComponent` 를 이용하여 Player의 Rigidbody2D를 가져옵니다.

![1%202742062629d646bcb65f0d7e4fc79683/Untitled%2013.png](1%202742062629d646bcb65f0d7e4fc79683/Untitled%2013.png)

이제 Player의 Rigidbody2D의 값을 조정할 수 있다.

### 플레이어 키 입력받기

```csharp
using UnityEngine;

public class PlayerMovement : MonoBehaviour
{
//앞에 이어서 적어주기
		void Update()
    {
        Move();
        Jump();
    }

    void Move()
    {
        Vector3 moveVelocity = Vector3.zero;

        if (Input.GetAxisRaw ("Horizontal") < 0)
        {
            moveVelocity = Vector3.left;
        }

        else if(Input.GetAxisRaw("Horizontal") > 0)
        {
            moveVelocity = Vector3.right;
        }

        transform.position += moveVelocity * movePower * Time.deltaTime;
    }
    void Jump()
    {
        if (isJumping == false)
        {
            if (Input.GetKeyDown("space"))
            {
                isJumping = true;
                Vector2 jumpVelocity = new Vector2(0, jumpPower);
                rigid.AddForce(jumpVelocity, ForceMode2D.Impulse);

            }

        }
        else return;
    }
}
```

먼저 `Update` 와 `FixedUpdate` 를 구분해 설명하겠습니다.

### **Update vs FixedUpdate**

### **Update**

- 프레임당 1회 호출
- 불규칙적으로 실행 (물리엔진 충돌검사 등이 제대로 안될 수 있음)
- 주로 단순한 타이머, 키 입력을 받을 때 사용

### **FixedUpdate**

- 고정적인 시간을 기준으로 반복
- 프레임에 기반하지 않아 물리 계산에 유리
- 주로 물리 효과가 적용된 오브젝트를 조정할 때 사용

### **LateUpdate(참고)**

- 위 Update 함수가 모두 호출 된 후, 마지막으로 호출
- 주로 오브젝트를 따라가는 카메라에 설정

**jump 구간**

**addforce란**

![1%202742062629d646bcb65f0d7e4fc79683/Untitled%2014.png](1%202742062629d646bcb65f0d7e4fc79683/Untitled%2014.png)

코드에 대해서 추가 설명하기

### 유니티 에디터 설정하기

rigidbody2D → freeze z

![1%202742062629d646bcb65f0d7e4fc79683/Untitled%2015.png](1%202742062629d646bcb65f0d7e4fc79683/Untitled%2015.png)

PlayerMovement스크립트 설정 → 필요시 이동속도 알아서 설정 ( Move : 4 , Jump : 8 )

![1%202742062629d646bcb65f0d7e4fc79683/Untitled%2016.png](1%202742062629d646bcb65f0d7e4fc79683/Untitled%2016.png)

### 점프 설정 바꾸기

 지금까지 제작한 게임을 테스트 해보면 점프 무한히 가능 → 한번만 점프할 수 있도록 바꾸기

점프 한번으로 바꾸기 → 앞의 block 태그 이용

```csharp
using UnityEngine;

public class PlayerMovement : MonoBehaviour
*{

    ...*

    private void OnCollisionEnter2D(Collision2D collision)
    {
        if (collision.gameObject.CompareTag("block"))
        {
            isJumping = false;
        }
    }
}
```

### 적 구현하기

적만들기  - sprite설정(96*128자르기), rigidbody(freezerotation), collider설정, tag →enemy

![1%202742062629d646bcb65f0d7e4fc79683/Untitled%2017.png](1%202742062629d646bcb65f0d7e4fc79683/Untitled%2017.png)

[]()

**적과 충돌시 대응하기**

Enemy와 충돌했을시 → Scene 재시작

```csharp
using UnityEngine;

public class PlayerMovement : MonoBehaviour
*{

   ...*

   private void OnCollisionEnter2D(Collision2D collision)
    {
        if (collision.gameObject.CompareTag("block"))
        {
            isJumping = false;
        }
        if (collision.gameObject.CompareTag("enemy"))
        {
            Hit();
        }
    }
    void Hit()
    {
        SceneManager.LoadScene(SceneManager.GetActiveScene().buildIndex);
    }
}
```

### 부드러운 카메라 무빙 적용하기

추가필요