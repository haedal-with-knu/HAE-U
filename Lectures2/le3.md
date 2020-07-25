[목록으로 돌아가기](L1.md)
# 플랫폼 게임 만들기 3

## 수업내용

- 안드로이드 어플 개발하기
    - Canvas란
    - 조이스틱 기능 추가하기
    - 스크립트 수정 및 보완하기
- 활용방안 생각하기

# 안드로이드 어플 개발하기

 현재까지 개발한 게임을 안드로이드 입으로 플랫폼을 옮겨 제작해 보겠습니다. 안드로이드 앱으로 변환시 입력받는 키가 키보드에서 터치로 변경된다는 점을 고려해주어야 합니다. 

 UI 기능을 사용하기 전에 캔버스에 대해 알아보겠습니다.

## Canvas란

 유니티에서 모든 UI 객체의 렌더링을 관리하기 위한 컴포넌트 입니다. 즉, 유니티의 모든 UI 구성 요소들은 캔버스 밑에 위치해야합니다. 캔버스의 UI요소는 계층 구조이므로 순서에 주의하여 배치해주어야합니다. 즉, 위에 배치된 UI가 두번째 UI에 가려 보이지 않게됩니다.

### Render Mode

**스크린 공간 - 오버레이**

가장 기본이 되는 모드로 모든 UI 요소가 제일 위에 렌더링 되는 경우입니다.

**스크린 공간 - 카메라**

캔버스가 씬의 특정 카메라에서 주어진 거리만큼 앞쪽에 위치합니다. UI요소를 원근감있게 렌더링 할 수 있습니다.

**월드 공간**
캔버스가 다른 게임오브젝트처럼 동작합니다.

![3%20e62ff36d3fea40409678d2a0ce50e897/Untitled.png](3%20e62ff36d3fea40409678d2a0ce50e897/Untitled.png)

## 조이스틱 기능 추가하기

 휴대폰에서 터치를 입력받기 위해 조이스틱 기능을 추가해보겠습니다.

먼저 UI를 배치할 Canvas를 생성해줍니다.

![3%20e62ff36d3fea40409678d2a0ce50e897/Untitled%201.png](3%20e62ff36d3fea40409678d2a0ce50e897/Untitled%201.png)

이후 받아두었던  grey_circle 이미지 파일을 이용하여 조이스틱 모양을 만들어주겠습니다.

![3%20e62ff36d3fea40409678d2a0ce50e897/Untitled%202.png](3%20e62ff36d3fea40409678d2a0ce50e897/Untitled%202.png)

Canvas안에 UI > Image로 background 이름의 이미지를 만들어줍니다.  
같은방법으로 background자녀 오브젝트로 joystick 이름의 이미지를 만들어줍니다.  

![3%20e62ff36d3fea40409678d2a0ce50e897/Untitled%203.png](3%20e62ff36d3fea40409678d2a0ce50e897/Untitled%203.png)

## 스크립트 수정 및 보완하기

이제 이 조이스틱을 컨트롤할 스크립트를 제작해보겠습니다. "Assets/ Scripts"에 **JoystickController.cs** 의 스크립트를 생성합니다.

![3%20e62ff36d3fea40409678d2a0ce50e897/Untitled%204.png](3%20e62ff36d3fea40409678d2a0ce50e897/Untitled%204.png)

### JoystickController 스크립트 코딩하기

```csharp
using System.Collections;
using System.Collections.Generic;
using Unity.Mathematics;
using UnityEngine;
using UnityEngine.EventSystems;

public class JoystickController : MonoBehaviour, IDragHandler, IPointerDownHandler, IPointerUpHandler

{
    public GameObject background;
    public GameObject joystick;

    private float background_radius;
    private Vector3 center;
    private Vector3 Axis;

    void Start()
    {
        center = this.transform.position;
        background_radius = background.GetComponent<RectTransform>().rect.width / 2;
    }

    void Update()
    {
        //Debug.Log(background_radius);
    }

    public void OnDrag(PointerEventData eventData)
    {
        Vector3 fingerPos = Input.mousePosition;

        Axis = (fingerPos - center).normalized;

        float fDistance = Vector3.Distance(fingerPos, center);
        if (fDistance > background_radius) joystick.transform.position = center + Axis * background_radius;
        else joystick.transform.position = center + Axis * fDistance;

        PlayerMovement.horizontal = Axis.x;
    }

    public void OnPointerDown(PointerEventData eventData)
    {
        joystick.transform.position = Input.mousePosition;
        Vector3 fingerPos = Input.mousePosition;

        Axis = (fingerPos - center).normalized;

        PlayerMovement.horizontal = Axis.x;
    }

    public void OnPointerUp(PointerEventData eventData)
    {
        joystick.transform.position = center;
        Axis = Vector3.zero;
        PlayerMovement.horizontal = 0;
    }

}
```

 이후 PlayerMovement.cs의 move메소드의 horizontal 관련 코드를 지워야 충돌없이 정상 작동 가능합니다.

 아래의 코드를 찾아 삭제해줍니다.

```jsx
       // horizontal = Input.GetAxis("Horizontal");
```

 마지막으로 "Canvas / background" 와 "Canvas / joystick"을 JoystickController과 연결해줍니다.

![3%20e62ff36d3fea40409678d2a0ce50e897/Untitled%205.png](3%20e62ff36d3fea40409678d2a0ce50e897/Untitled%205.png)

# 기타 활용방안 생각해보기

 예시에선 간단한 플랫폼 게임 만들기를 따라 해보고 새로운 기능들을 추가해보았습니다. 지금까지 배운 내용을 바탕으로 플랫폼 게임에 새로운 기능을 더 추가할 수도 있고 새로운 게임을 만들어 보실 수도 있습니다. 각자 자신의 아이디어를 내보고 적용해봅시다.

 다음은 활용방안 예시입니다.

## 활용방안

- 새로운 공격 모션 만들기
- 스킬 모션 만들기
- 피격 이펙트 만들기
- 원거리 공격 추가
- 중력 에 효과주기( 더블점프, 중력바꾸기)
- 점수 or 체력 UI 만들기

[목록으로 돌아가기](L1.md)
