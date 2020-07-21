# 플랫폼 게임만들기 2

## 수업내용

- 이동 애니메이션 구현하기
    - 애니메이터 컨트롤러
    - 이동 애니메이션 생성하기
    - 애니메이터 컨트롤러 사용하기
- 점프 애니메이션 구현하기
    - 점프 애니메이션 생성하기
    - RayCast기능 알아보기
    - RayCast를 활용하여 애니메이션 적용하기
- 공격 애니메이션 구현하기
    - 공격 애니메이션 생성하기
    - 공격 딜레이 만들기

# 이동 애니메이션 구현하기

## 애니메이터 컨트롤러

### 파라미터 관리

![2%201fb3e014c12e40cfaa2dec0258be68e9/Untitled.png](2%201fb3e014c12e40cfaa2dec0258be68e9/Untitled.png)

**Parameters**옆의 + 아이콘을 클릭하면

Float, Int, Bool, Trigger를 추가할 수 있으며 애니메이션의 퀄리티나 조건을 나타냅니다.

후에 c#스크립트에서 가져와서 관리 및 컨트롤 할 수 있습니다.

### **Animator Window** 살펴보기

애니메이터 창에서 애니메이터 컨트롤러 상태를 설정할 수가 있습니다.

오른쪽 키를 눌러 make Transition을 사용하여 각 상태간의 관계(화살표)를 설정할 수 있습니다.

![2%201fb3e014c12e40cfaa2dec0258be68e9/Untitled%201.png](2%201fb3e014c12e40cfaa2dec0258be68e9/Untitled%201.png)

처음 생성된 상태는 기본상태(주황색)로 됩니다.

(기본을 변경하고 싶으면 원하는 상태에서 마우스 오른쪽 -> **Set As Default**)

### 인스펙터 창

상태 편집은 클릭하면 인스펙터창에서 할 수 있습니다.

![2%201fb3e014c12e40cfaa2dec0258be68e9/Untitled%202.png](2%201fb3e014c12e40cfaa2dec0258be68e9/Untitled%202.png)

**speed** 

- 일반 애니메이션 속도의 비해 얼마나 빠르게 재생되는지를 참조

**Mirror** 

- 애니메이션의 좌우가 반전

**Foot IK** 

- 체크하면 애니메이션이 발 미끄러짐이 감소하거나 제거 된다.

**Transitions** 

- 다른 상태로 트랜지션할 수있는 상태를 표시,설정

트랜지션 상태 (흰 화살표)

[https://lh3.googleusercontent.com/jSW2vG4cN5Sns_Z1yWiQJXncpvhif1wRCytoBN2lCBO_Au6FNJ4yKtLGchfXhQy1j81kKtOZKzT-b5fpS8KykBRDqJaH5pWrfnWLHa-7Cvl7QJ_DpozCHYM42Ba06o4-_r4_a1o9](https://lh3.googleusercontent.com/jSW2vG4cN5Sns_Z1yWiQJXncpvhif1wRCytoBN2lCBO_Au6FNJ4yKtLGchfXhQy1j81kKtOZKzT-b5fpS8KykBRDqJaH5pWrfnWLHa-7Cvl7QJ_DpozCHYM42Ba06o4-_r4_a1o9)

## 이동 애니메이션 생성하기

### 움직임 애니메이션

원하는 이동 애니메이션에 사용할 이미지들을 다중 선택하고 Hierarchy 창에 드래그 앤 드롭하면 animation파일이 생성됩니다. 이를 Assets/Animations 폴더에 **player_move.anim** 로 이름을 정하고 저장합니다. 

 움직임은 계속 반복되어야 하므로 **LoopTime을 체크**하여 애니메이션이 반복되게 합니다. Animations 폴더에 원하는 파일이 만들어졌으므로 Hierarchy에 생성된 오브젝트는 삭제해줍니다.

![2%201fb3e014c12e40cfaa2dec0258be68e9/Untitled%203.png](2%201fb3e014c12e40cfaa2dec0258be68e9/Untitled%203.png)

![2%201fb3e014c12e40cfaa2dec0258be68e9/Untitled%204.png](2%201fb3e014c12e40cfaa2dec0258be68e9/Untitled%204.png)

 

### 서 있는 애니메이션

 이제 서 있는 애니메이션을 만들어보겠습니다. 하나의 이미지로 설정해도 되지만 애니메이션 기능을 활용하기 위해 간단히 2가지 이미지를 이용하여 만들어보겠습니다. 

 마찬가지로 "Assets/Animations" 폴더에 **player_idle.anim** 로 이름을 정하고 저장합니다. 움직임은 계속 반복되어야 하므로 **LoopTime을 체크**하여 애니메이션이 반복되게 합니다. player_move.anim과 마찬가지로 Hierarchy에 생성된 오브젝트는 삭제해줍니다.

![2%201fb3e014c12e40cfaa2dec0258be68e9/Untitled%205.png](2%201fb3e014c12e40cfaa2dec0258be68e9/Untitled%205.png)

![2%201fb3e014c12e40cfaa2dec0258be68e9/Untitled%206.png](2%201fb3e014c12e40cfaa2dec0258be68e9/Untitled%206.png)

### 애니메이터 컨트롤러 만들기

 Animations에 player의 움직임을 제어할 수 있게 Create > Animator Controller로 **player_anim**의 이름으로 Animator Controller을 만들어줍니다. 

![2%201fb3e014c12e40cfaa2dec0258be68e9/Untitled%207.png](2%201fb3e014c12e40cfaa2dec0258be68e9/Untitled%207.png)

 아까 만들어 두었던 애니메이션 파일들을 Drag&Drop으로 Animator 창으로 옮겨줍니다. 여기까지 완료하면 애니메이터 컨트롤러를 사용하기 위한 기본적인 설정이 완료됩니다.

![2%201fb3e014c12e40cfaa2dec0258be68e9/Untitled%208.png](2%201fb3e014c12e40cfaa2dec0258be68e9/Untitled%208.png)

### 애니메이터 컨트롤러 적용하기

마지막으로 Player 오브젝트에 드래그 앤 드롭으로 Animator Controller을 적용시켜줍니다.

![2%201fb3e014c12e40cfaa2dec0258be68e9/Untitled%209.png](2%201fb3e014c12e40cfaa2dec0258be68e9/Untitled%209.png)

## 애니메이터 컨트롤러 사용하기

### 애니메이션 속도 조정하기

 이동이 없을 경우 애니메이션을 천천히 변환하고 싶기 때문에 Inspector에서 속도를 0.1로 줄여줍니다.

![2%201fb3e014c12e40cfaa2dec0258be68e9/Untitled%2010.png](2%201fb3e014c12e40cfaa2dec0258be68e9/Untitled%2010.png)

### 애니메이터 변수 관리하기

애니메이터 컨트롤러에서 상태 변화를 감지하기 위해서 Parameters에 isMove라는 Bool 값을 추가해줍니다.

![2%201fb3e014c12e40cfaa2dec0258be68e9/Untitled%2011.png](2%201fb3e014c12e40cfaa2dec0258be68e9/Untitled%2011.png)

### 애니메이터 트랜지션 만들기

plater_idle과 plater_move 상호간의 모션을 설정하기위해 Make Transition을 이용하여 양방향 Transition을 만들어줍니다.

![2%201fb3e014c12e40cfaa2dec0258be68e9/Untitled%2012.png](2%201fb3e014c12e40cfaa2dec0258be68e9/Untitled%2012.png)

![2%201fb3e014c12e40cfaa2dec0258be68e9/Untitled%2013.png](2%201fb3e014c12e40cfaa2dec0258be68e9/Untitled%2013.png)

### **애니메이션 변환간 딜레이 없게하기 (양방향 다 적용해주기)**

Has Exit Time 체크 해제한 뒤 Transition Duration 값을 0으로 두어 애니메이션 변환간 딜레이를 없애줍니다.

![2%201fb3e014c12e40cfaa2dec0258be68e9/Untitled%2014.png](2%201fb3e014c12e40cfaa2dec0258be68e9/Untitled%2014.png)

### **Transition 조건 변경하기**

 Transition 조건을 앞에서 만든 isMove를 이용하여 조건을 설정해 줍니다. 나중에 스크립트에 isMove 변수를 조정하여 애니메이션을 서로 간에 변환할 수 있게 합니다. 아래 그림과 같이 idle에서 move로 이동할 조건은 isMove 가 true, move에서 idle로 이동할 조건은 isMove가 false로 설정해 줍니다.

![2%201fb3e014c12e40cfaa2dec0258be68e9/Untitled%2015.png](2%201fb3e014c12e40cfaa2dec0258be68e9/Untitled%2015.png)

### **스크립트에 적용하기**

 위에서 설정한 `isMove`를 사용하기 위해 PlayerMovement.cs의 **Move메서드**를 수정해줍니다. 이동을 하고 있을 경우 `isMove`를 true로, 그렇지 않을경우 false로 둡니다.  또한 이미지 뒤집기를 사용하기위해 `SpriteRenderer`을 가져와서 사용합니다.

```csharp
public class PlayerMovement : MonoBehaviour
{
    ...

    private Animator anim;
    private SpriteRenderer renderer;

		void Start()
    {
        rigid = gameObject.GetComponent<Rigidbody2D>();
        anim = GetComponent<Animator>();
        renderer = gameObject.GetComponent<SpriteRenderer>();
    }

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
        if (horizontal < 0)
        {
            renderer.flipX = true;
            anim.SetBool("isMove", true);
        }

        else if (horizontal > 0)
        {
            renderer.flipX = false;
            anim.SetBool("isMove", true);
        }
        else
        {
            anim.SetBool("isMove", false);
        }
        transform.position += moveVelocity * movePower * Time.deltaTime;
    }
```

실행결과 이동시 좌 우 이미지 뒤집기와 애니메이션이 잘 적용되는지 확인할 수 있습니다. 

![2%201fb3e014c12e40cfaa2dec0258be68e9/Untitled%2016.png](2%201fb3e014c12e40cfaa2dec0258be68e9/Untitled%2016.png)

# 점프 애니메이션 만들기

## 점프 애니메이션 생성하기

### 애니메이션 생성하기

 점프 애니메이션을 만들어보겠습니다. 간단히 2가지 이미지를 이용하여 만들어보겠습니다. 마찬가지로 Assets/Animations 폴더에 **player_jump.anim** 로 이름을 정하고 저장합니다. player_move.anim과 마찬가지로 Hierarchy에 생성된 오브젝트는 삭제해줍니다.

![2%201fb3e014c12e40cfaa2dec0258be68e9/Untitled%2017.png](2%201fb3e014c12e40cfaa2dec0258be68e9/Untitled%2017.png)

### 애니메이터 변수 관리하기

Animator에 player_jump를 추가해줍니다. Parameter도 isJump를 추가해준 뒤 player_jump 속도를 0.2로 설정해줍니다. 각자 설정에 맞게 자연스러운 애니메이션을 위한 속도를 설정해주셔도 좋습니다.

 마찬가지로 Has Exit Time를 체크 해제하고 Transition Duration 를 0으로 설정해줍니다.

![2%201fb3e014c12e40cfaa2dec0258be68e9/Untitled%2018.png](2%201fb3e014c12e40cfaa2dec0258be68e9/Untitled%2018.png)

### 애니메이션 스크립트에 적용하기

여기서 주의할 점은 앞에선 점프 여부 확인을 위해 isJumping를 사용하였지만 이제는 anim.isJump 를 사용한다는 점입니다. 아래는 수정한 스크립트 코드입니다.

```jsx
using UnityEngine;
using UnityEngine.SceneManagement;

public class PlayerMovement : MonoBehaviour
{

    ...

		void Update()
    {
        Move();
        Jump();
        isLanding();
    }
		void Move()
    {
				...
		}
    void Jump()
    {
        if (anim.GetBool("isJump")==false)
        {
            if (Input.GetKeyDown("space"))
            {
                anim.SetBool("isJump", true);
                Vector2 jumpVelocity = new Vector2(0, jumpPower);
                rigid.AddForce(jumpVelocity, ForceMode2D.Impulse);

            }
        }
        else return;
    }

		...

		private void OnCollisionEnter2D(Collision2D collision)
    { 
				if (collision.gameObject.CompareTag("block"))
        {
            anim.GetBool("isJump")=false
        }
        if (collision.gameObject.CompareTag("enemy"))
        {
            Hit();
        }
    }

		...

}
```

실행결과 점프 애니메이션이 잘 구현된 것을 확인할 수 있습니다.

![2%201fb3e014c12e40cfaa2dec0258be68e9/Untitled%2019.png](2%201fb3e014c12e40cfaa2dec0258be68e9/Untitled%2019.png)

### RayCast기능 알아보기

RayCast란 RayCast 스크립팅을 가진 게임 오브젝트 원점에서 설정한 방향으로 Ray를 날려 설정한 거리 이내에 물체가 있는지 출동감지를 해주는 방식을 말합니다.

![2%201fb3e014c12e40cfaa2dec0258be68e9/Untitled%2020.png](2%201fb3e014c12e40cfaa2dec0258be68e9/Untitled%2020.png)

출처 [https://docs.unity3d.com/kr/530/ScriptReference/Physics.Raycast.html](https://docs.unity3d.com/kr/530/ScriptReference/Physics.Raycast.html)

### RayCast를 활용하여 애니메이션 적용하기

 지금까지 collision을 이용하여 플레이어와 블럭의 충돌을 확인했습니다. 이 방법은 만들기 쉽다는 장점이 있지만 블럭이 아래에 있을 때 뿐 아니라 **위, 양옆 모두 접촉만 하고 있다면 점프를 다시 할 수 있는 문제** 가 있습니다. 

 아래와 같은 상황에서도 땅 위에 서 있다고 판단하여 점프가 가능한 문제가 발생합니다.

![2%201fb3e014c12e40cfaa2dec0258be68e9/Untitled%2021.png](2%201fb3e014c12e40cfaa2dec0258be68e9/Untitled%2021.png)

 

 따라서 collision 대신 **RayCast방법**을 이용해보겠습니다. PlayerMovement 스크립트를 수정해봅시다.  땅에 닿은지 확인하기 위한 **isLanding메서드** 도 추가하겠습니다. 앞의 block과의 collision 코드는 삭제해주어야 합니다.

 RayCast에서 block인지 판단하기 위하여 block 오브젝트의 **Layer을 block으로 설정**해줍니다. Layer 설정 방법은 플랙폼 게임만들기 1강 태그 관리 부분을 참고해줍니다.

![2%201fb3e014c12e40cfaa2dec0258be68e9/Untitled%2022.png](2%201fb3e014c12e40cfaa2dec0258be68e9/Untitled%2022.png)

```csharp
using UnityEngine;
using UnityEngine.SceneManagement;

public class PlayerMovement : MonoBehaviour
{

    ...

		void Update()
    {
        Move();
        Jump();
        isLanding();
    }
		void Move()
    {
				...
		}
    void Jump()
    {
       ...
    }

    void isLanding()
    {
        if (rigid.velocity.y <= 0)
        {
						RaycastHit2D rayHit = Physics2D.Raycast(rigid.position, Vector3.down,1,LayerMask.GetMask("block"));
            if(rayHit.collider != null)
            {
                if (rayHit.distance < 0.8f)
                    anim.SetBool("isJump", false);
            }
        }
    }

		private void OnCollisionEnter2D(Collision2D collision)
    {
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

실행결과 정상적으로 아래에 블럭이 있을경우만 점프를 할 수 있음을 확인할 수 있습니다.