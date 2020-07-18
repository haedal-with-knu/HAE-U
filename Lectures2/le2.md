# 플랫폼 게임만들기 2

## 수업내용

- 이동 애니메이션 구현하기
    - 유니티 애니메이션
    - 이동 애니메이션 생성하기
    - 애니메이터 컨트롤러 사용하기
- 점프 애니메이션 구현하기
    - 점프 애니메이션 생성하기
    - RayCast기능 알아보기
    - RayCast를 활용하여 애니메이션 적용하기
- 공격 애니메이션 구현하기
    - 공격 애니메이션 생성하기
    - 공격 딜레이 만들기

## 이동 애니메이션 구현하기

### 유니티 애니메이션

 기본적인 내용 추가

애니메이션 과 애니메이션 컨트롤러에 관하여.

### 이동 애니메이션 생성하기

![2%20138ef6beb1ca42b59a3fd43e6954ab34/Untitled.png](2%20138ef6beb1ca42b59a3fd43e6954ab34/Untitled.png)

원하는 이동 애니메이션에 사용할 이미지들을 다중 선택하고 Scene에 Drag&Drop하면 animation파일이 생성됩니다. 이를 Assets/Animations 폴더에 player_move.anim 로 이름을 정하고 저장합니다.

![2%20138ef6beb1ca42b59a3fd43e6954ab34/Untitled%201.png](2%20138ef6beb1ca42b59a3fd43e6954ab34/Untitled%201.png)

 이후 Animations에 player의 움직임을 제어할 수 있게 Create>Animator Controller로 player_anim의 이름으로 Animator Controller을 만들어줍니다.

![2%20138ef6beb1ca42b59a3fd43e6954ab34/Untitled%202.png](2%20138ef6beb1ca42b59a3fd43e6954ab34/Untitled%202.png)

아까 만들어 두었던 애니메이션 파일들을 Drag&Drop으로 Animator 창으로 옮겨줍니다.

### 애니메이터 컨트롤러 사용하기

## 점프 애니메이션 만들기

### 점프 애니메이션 생성하기

### RayCast기능 알아보기

### RayCast를 활용하여 애니메이션 적용하기

## 공격 애니메이션 구현하기

### 공격 애니메이션 생성하기

### 공격 딜레이 만들기

시간 설정 

player_idle :0.1 

player_move : 1

player_jump : 0.2

사용변수(bool)

isMove

isJump

RayCast이용 바닥 확인

Raycast란

[https://docs.unity3d.com/kr/530/ScriptReference/Physics.Raycast.html](https://docs.unity3d.com/kr/530/ScriptReference/Physics.Raycast.html)

```csharp
using UnityEngine;
using UnityEngine.SceneManagement;

public class PlayerMovement : MonoBehaviour
{
    public float movePower = 1f;
    public float jumpPower = 1f;

    Rigidbody2D rigid;

    Vector3 movement;
    private Animator anim;
    private SpriteRenderer renderer;

    void Start()
    {
        rigid = gameObject.GetComponent<Rigidbody2D>();
        anim = GetComponent<Animator>();
        renderer = gameObject.GetComponentInChildren<SpriteRenderer>();
    }
    void FixedUpdate()
    {
        Move();
        Jump();
        isLanding();
    }

    void Move()
    {
        Vector3 moveVelocity = Vector3.zero;

        if (Input.GetAxisRaw("Horizontal") < 0)
        {
            renderer.flipX = true;
            anim.SetBool("isMove", true);
            moveVelocity = Vector3.left;
        }

        else if (Input.GetAxisRaw("Horizontal") > 0)
        {
            renderer.flipX = false;
            anim.SetBool("isMove", true);
            moveVelocity = Vector3.right;
        }
        else
        {
            anim.SetBool("isMove", false);
        }
        transform.position += moveVelocity * movePower * Time.deltaTime;
    }
    void Jump()
    {

      //  rigid.velocity = Vector2.zero;
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

    void isLanding()
    {
        if (rigid.velocity.y < 0)
        {
            Debug.DrawRay(rigid.position, Vector3.down, new Color(1, 1, 1)); //ray시각으로 확인용
            RaycastHit2D rayHit = Physics2D.Raycast(rigid.position, Vector3.down,1,LayerMask.GetMask("block"));
            if(rayHit.collider != null)
            {
                if (rayHit.distance < 0.7f)
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