# 플랫폼 게임만들기 1

## 수업내용

- 수업 정보
- 기초 설정과 준비
    - 게임 생성하기
    - 필요 리소스 다운하기
    - 스프라이트 관리하기
- 기본 요소 관리하기
    - 오브젝트 생성하기
    - 카메라 설정
    - physics 2D 설정
    - 플레이어와 블럭 생성하기
- 본격적인 프로그래밍 들어가기
    - c# 스크립트란
    - 플레이어 움직임 코딩하기
    - 플레이어 키 입력받기
    - 유니티 에디터 설정하기
    - 점프 설정 바꾸기
    - 적 구현하기
    - 적과 충돌 시 대응하기

# 수업정보

수업자료 참고 : DoggyHouse 블로그, c#프로그래밍 교재, 

수업 소스 출처 : kenny's source

# **기초 설정과 준비**

## **게임 생성하기**

템플릿 : 2D

버젼 : 19.4.2f

![1%2049ea631606ec47418c66e46dce0c1884/Untitled.png](1%2049ea631606ec47418c66e46dce0c1884/Untitled.png)

## **필요 리소스 다운하기**

### 게임에 필요한 소스 다운로드

[플랫폼 소스](https://drive.google.com/file/d/1u9d4ZUz6Asm2k-KTZbMdrzT-3i6U0gDu/view?usp=sharing)

### 사용할 리소스 불러오기

  "Assets / Images" 에 알집 안의 파일 드래그 앤 드롭으로 불어올 수 있습니다.

![1%2049ea631606ec47418c66e46dce0c1884/Untitled%201.png](1%2049ea631606ec47418c66e46dce0c1884/Untitled%201.png)

## 스프라이트 관리하기

### **Sprite 정보창**

**SpriteMode : Multiple**    

- 이미지 자를지 여부 설정 가능합니다.

**SpriteEditor**    

- 세부 sprite 설정용 입니다.

**FilterMode : Point**    

- 비트이미지 뭉개지지 않게 설정 가능합니다.

![1%2049ea631606ec47418c66e46dce0c1884/Untitled%202.png](1%2049ea631606ec47418c66e46dce0c1884/Untitled%202.png)

### **Sprite Editor란**

**Grid By Cell Size**

- 각 sprite가 일정한 크기일 경우 이용합니다.

**Automatic** 

- 각 sprite를 원하는 크기로 따로따로 자를 경우 이용합니다.

일정한 크기로 자르고 싶으므로 grid by cell size로 **X=96, Y=128**로 크기설정  하겠습니다.

![1%2049ea631606ec47418c66e46dce0c1884/Untitled%203.png](1%2049ea631606ec47418c66e46dce0c1884/Untitled%203.png)

하나의 이미지를 손쉽게 잘라서 관리할 수 있다.

### 주의사항

- spriteEditor 실행 안될시 PacakageManager이용하기

![1%2049ea631606ec47418c66e46dce0c1884/Untitled%204.png](1%2049ea631606ec47418c66e46dce0c1884/Untitled%204.png)

# 기본요소 관리하기

## 오브젝트 생성하기

원하는 이미지 파일을 Hierarchy에 드래그 앤 드롭으로 손쉽게 오브젝트를 생성 가능합니다.

![1%2049ea631606ec47418c66e46dce0c1884/Untitled%205.png](1%2049ea631606ec47418c66e46dce0c1884/Untitled%205.png)

## 카메라 설정

### 카메라 설정값

 **size** =4 , 원하는 배경 색, Position Z 주의하기

### 주의사항

- 카메라 설정시 position Z가 중요합니다.  카메라가 오브젝트보다 앞에있으면(z값이 크면) 오브젝트가 게임 화면에 나타나지 않을 수 있음을 주의해줍니다.

![1%2049ea631606ec47418c66e46dce0c1884/Untitled%206.png](1%2049ea631606ec47418c66e46dce0c1884/Untitled%206.png)

## Physics 2D 설정

file → build settings → player settings → physics 2D에서 **Gravity Y = -20** 로 설정해줍니다.

예시에선 -20의 값으로 설정하였지만 각자 직접 테스트 해보고 적당한 값을 적용해도 괜찮습니다.

![1%2049ea631606ec47418c66e46dce0c1884/Untitled%207.png](1%2049ea631606ec47418c66e46dce0c1884/Untitled%207.png)

![1%2049ea631606ec47418c66e46dce0c1884/Untitled%208.png](1%2049ea631606ec47418c66e46dce0c1884/Untitled%208.png)

## 플레이어와 블럭 생성하기

### **Player**

1. RigidBody2D 설정 → Freeze Rotation z해주기
2. BoxCollider 2D 설정 → Edit Collider로 충돌범위 조정

### **Block**

1. RigidBody2D 설정 → Freeze Rotation, Position 모두 해주기
2. BoxCollider 2D 설정 → Edit Collider로 충돌범위 조정
3. 태그붙이기
4. 앞으로 자주 사용할 것이므로 prefabs설정하기

플레이어 경우 constraint의 z값을 고정시켜 멋대로 회전하지 않게 설정해줍니다.

![1%2049ea631606ec47418c66e46dce0c1884/Untitled%209.png](1%2049ea631606ec47418c66e46dce0c1884/Untitled%209.png)

block경우 constraint의 x,y,z값을 고정하여 중력에 의해 움직이지 않도록 해줍니다.

![https://user-images.githubusercontent.com/48755297/87399167-ef409a00-c5f1-11ea-8be6-fdd5ea586b32.png](https://user-images.githubusercontent.com/48755297/87399167-ef409a00-c5f1-11ea-8be6-fdd5ea586b32.png)

### **Rigidbody 2D란**

- Rigidbody란 강체(剛體)라는 뜻으로, 유니티에서 질량, 중력 등 물리적인 기능을 가지게 해주는 것입니다.

### **Collider 2D란**

- Collider란 오브젝트의 충돌 '범위' 를 지정해주는 것입니다.

### 태그붙이는 과정

 Inspector창의 이름 밑의 Tag에서 Tag를 관리할 수 있습니다. 제일 밑의 AddTag를 이용하면 원하는 이름의 새로운 태그를 만드는 것도 가능합니다. 그 옆의 Layer도 같은 방법으로 추가 및 관리가 가능합니다.

![1%2049ea631606ec47418c66e46dce0c1884/Untitled%2010.png](1%2049ea631606ec47418c66e46dce0c1884/Untitled%2010.png)

![1%2049ea631606ec47418c66e46dce0c1884/Untitled%2011.png](1%2049ea631606ec47418c66e46dce0c1884/Untitled%2011.png)

![1%2049ea631606ec47418c66e46dce0c1884/Untitled%2012.png](1%2049ea631606ec47418c66e46dce0c1884/Untitled%2012.png)

# 본격적인 프로그래밍 들어가기

## **c#스크립트란?**

c#스크립트란 c++의 강력함 + VB의 편리함 + JAVA의 독립적 플랫폼 장점들을 모두 모은 유니티에서 사용하는 언어입니다.

## 플레이어 움직임 코딩하기

Assets에 Scripts폴더 추가 후 **PlayerMovement.cs** 의 이름으로 c#스크립트를 만들어줍니다.

![1%2049ea631606ec47418c66e46dce0c1884/Untitled%2013.png](1%2049ea631606ec47418c66e46dce0c1884/Untitled%2013.png)

### 주의점

Scripts 폴더에 C# 스크립트 생성후 수정시 class이름과 파일 이름이 같은지 항상 확인해야 오류를 방지할 수 있습니다.

![https://user-images.githubusercontent.com/48755297/87399640-9e7d7100-c5f2-11ea-9bdb-6b017ba37cf2.png](https://user-images.githubusercontent.com/48755297/87399640-9e7d7100-c5f2-11ea-9bdb-6b017ba37cf2.png)

### 코딩 시작하기

처음에는 천천히 따라 적어가며 c#스크립트에 대해 알아봅시다.

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

위의 코드를 이용하면 아래의 Inspector의 Rigidbody2D기능을 가져와 사용할 수 있습니다.

![1%2049ea631606ec47418c66e46dce0c1884/Untitled%2014.png](1%2049ea631606ec47418c66e46dce0c1884/Untitled%2014.png)

## 플레이어 키 입력받기

 플레이어의 키를 입력받기 위해 위의 **Start 메서드** 뒤에 이어서 코딩해줍니다.

부드러운 움직임을 위해 `GetAxis`를 사용했습니다.

```csharp
using UnityEngine;

public class PlayerMovement : MonoBehaviour
{
		public static float horizontal
		
		 ...
	    
		void Update()
    {
        Move();
        Jump();
    }

    void Move()
    {
        Vector3 moveVelocity = Vector3.zero;
        horizontal = Input.GetAxis("Horizontal");
        moveVelocity = horizontal * Vector3.right;

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

**Update**

- 프레임당 1회 호출
- 불규칙적으로 실행 (물리엔진 충돌검사 등이 제대로 안될 수 있음)
- 주로 단순한 타이머, 키 입력을 받을 때 사용

**FixedUpdate**

- 고정적인 시간을 기준으로 반복
- 프레임에 기반하지 않아 물리 계산에 유리
- 주로 물리 효과가 적용된 오브젝트를 조정할 때 사용

**LateUpdate(참고)**

- 위 Update 함수가 모두 호출 된 후, 마지막으로 호출
- 주로 오브젝트를 따라가는 카메라에 설정

### GetAxis vs GetAxisRaw

**Input.GetAxis(string name)**

- 1.0f 부터 1.0f 까지의 범위의 값을 반환한다. 즉, 부드러운 이동이 필요한 경우에 사용된다.

**Input.GetAxisRaw(string name)**

- 1, 0, 1 세 가지 값 중 하나가 반환된다. 키보드 값을 눌렀을 때 즉시 반응해야한다면 GetAxisRaw를 사용하면 된다.

### Rigidbody를 이용한 점프

 AddForce는 물리엔진의 rigid body를 이용해 움직입니다. 위로 힘을 가한 후 자연스럽게 중력에 의해 떨어지는것을 이용하여 점프를 만들 예정이므로 AddForce의 방법을 사용했습니다.

 아래는 ForceMode와 다양한 포커스모드에 관한 설명입니다.

![1%2049ea631606ec47418c66e46dce0c1884/Untitled%2015.png](1%2049ea631606ec47418c66e46dce0c1884/Untitled%2015.png)

마지막으로 스크립트를 플레이어 오브젝트에 드래그 앤 드롭하여 적용해줍니다.

![1%2049ea631606ec47418c66e46dce0c1884/Untitled%2016.png](1%2049ea631606ec47418c66e46dce0c1884/Untitled%2016.png)

## 유니티 에디터 설정하기

앞의 public 코드로 PlayerMovement 스크립트를 유니티 에디터에서 수정 가능합니다. 예시에선 Move : 4 , Jump : 8 로 두었지만 각자 마음대로 원하는 값을 설정 해 주어도 좋습니다.

![1%2049ea631606ec47418c66e46dce0c1884/Untitled%2017.png](1%2049ea631606ec47418c66e46dce0c1884/Untitled%2017.png)

### 유니티 에디터

- Property 값들을 설정할 수 있는 패널을 뜻합니다.
- 기본적으로 유니티 내 게임 오브젝트에 스크립트를 부착하고 그 안에 클래스들의 변수들이 public으로 설정되어 있으면 하나의 인스펙터로 구분, 관리할 수 있습니다.

 이제 오브젝트들을 적절히 배치하여 캐릭터의 움직임을 테스트해볼 수 있습니다.

![1%2049ea631606ec47418c66e46dce0c1884/Untitled%2018.png](1%2049ea631606ec47418c66e46dce0c1884/Untitled%2018.png)

## 점프 설정 바꾸기

 지금까지 제작한 게임을 테스트해 보면 점프키를 누대로 무한히 점프가 가능한 상태입니다. 이를 다시 땅에 닿기 전까지 한 번만 점프할 수 있게 만들어보겠습니다. 이를 위해서 앞서 block 오브젝트의 설정해둔 태그를 이용할 예정입니다. 

 현재까지 제작한 게임을 테스트해 보면 점프키를 여러 번 누르면 화면 밖까지 캐릭터가 날아갑니다...

![1%2049ea631606ec47418c66e46dce0c1884/Untitled%2019.png](1%2049ea631606ec47418c66e46dce0c1884/Untitled%2019.png)

 앞서 작성한 코드 뒤에 이어서 작성해주겠습니다.

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

`CompareTag`를 이용하여 block태그를 가진 오브젝트와 부딧쳤으면 `isJumping` 변수를 false로 두어 점프 중이 아니라고 판단하게 됩니다. 앞의 코드에서 `isJumping`이 false인 경우만 점프키를 인식할 수 있게 하였으므로 연속으로 점프 가능한 현상을 고칠 수 있습니다.

 테스트 결과 정상적으로 한 번만 점프할 수 있어 화면 밖으로 날아가지 않습니다.

![1%2049ea631606ec47418c66e46dce0c1884/Untitled%2020.png](1%2049ea631606ec47418c66e46dce0c1884/Untitled%2020.png)

## 적 구현하기

 앞서 만든 캐릭터와 같은 방법으로 적 오브젝트를 만들어보겠습니다. 먼저 캐릭터와 마찬가지로 sprite를 관리해줍니다 (SpriteEditor를 이용하여 96*128로 분할하기). 

만들어진 이미지를 드래그 앤 드롭하여 적 오브젝트를 만들고 RigidBody2D, Collider 2D 모두 똑같이 적용해줍니다. 단 플레이어와 달리 enemy라는 태그를 만들어 달아줍니다.

 자세한 내용이 기억이 나지 않는다면 위의 플레이어와 블럭 생성하기를 참고하시기 바랍니다.

![1%2049ea631606ec47418c66e46dce0c1884/Untitled%2021.png](1%2049ea631606ec47418c66e46dce0c1884/Untitled%2021.png)

## **적과 충돌 시 대응하기**

 적과 충돌 시 Scene을 재시작하도록 설정해보겠습니다. Scene을 관리하기위해선 SceneManager을 사용해야 하는데, 이를 위해서 코드 제일 윗줄에서 `using UnityEngine.SceneManagerment` 를 추가해주어야 합니다. 

```csharp
using UnityEngine;
using UnityEngine.SceneManagement;

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