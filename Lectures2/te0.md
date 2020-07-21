# 테트리스 만들기 0

## 수업내용

- c# 스크립트알아보기
    - c# 스크립트란
    - 기본적인 유니티 스크립트 구성요소
    - Start 와 Awake 비교하기
    - Update 와 FixedUpdate 비교하기
- c# 스크립트 이용한 게임 예시

# **c# 스크립트 알아보기**

### **c#스크립트란?**

c#스크립트란 c++의 강력함 + VB의 편리함 + JAVA의 독립적 플랫폼 장점들을 모두 모은 유니티에서 사용하는 언어입니다.UNITY의 c#스크립트의 기본적인 구성을 알아봅시다.

### **기본적인 유니티 스크립트 구성**

![https://user-images.githubusercontent.com/48755297/87387561-eba31800-c5dd-11ea-9c28-a84cfe71b553.png](https://user-images.githubusercontent.com/48755297/87387561-eba31800-c5dd-11ea-9c28-a84cfe71b553.png)

 스크립트 생성시 처음 볼 수 있는 화면. 필요한 코드를 제외하고 지우고 시작하는 것이 좋습니다.

 위의 코드를 살펴보면, 첫줄의 `using` 은 다른 lib의 코드를 import하는 기능이며 `public class` 는 자바의 객체 역할을, 마지막으로 `void Start()` 는 자바의 메소드를 의미합니다.

스크립트를 실행하면 Start(실행 시)와 Update(실행 중)메소드 안에 작성한 스크립트 코드가 실행됩니다.

![https://user-images.githubusercontent.com/48755297/87387400-91a25280-c5dd-11ea-80c2-43a64b577b52.png](https://user-images.githubusercontent.com/48755297/87387400-91a25280-c5dd-11ea-80c2-43a64b577b52.png)

### MonoBehaviour

- 모든 스크립트가 상속받는 기본 클래스입니다.

### Start  **vs  Awake 비교하기**

**Start**

- 게임이 시작되고 첫 번째 프레임 업데이트 이전에 실행됩니다.

**Awake**

- 오브젝트가 생성된 직후 실행합니다.

### **Update  vs  FixedUpdate 비교하기**

**Update**

- 프레임당 1회 호출합니다.
- 불규칙적으로 실행합니다. (물리엔진 충돌검사 등이 제대로 안될 수 있음)
- 주로 단순한 타이머, 키 입력을 받을 때 사용합니다.

**FixedUpdate**

- 고정적인 시간을 기준으로 반복합니다.
- 프레임에 기반하지 않아 물리 계산에 유리합니다.
- 주로 물리 효과가 적용된 오브젝트를 조정할 때 사용합니다.

**LateUpdate(참고)**

- 위 Update 함수가 모두 호출 된 후, 마지막으로 호출합니다.
- 주로 오브젝트를 따라가는 카메라에 설정합니다.

### On 계열 함수

**OnMouse-**

- 마우스의 인터랙션에 관련된 함수 집합. 마우스가 처음 올라왔을때, 나갔을때, 눌렀을때 등의 다양한 행동을 관리할 수 있습니다.

**OnTrigger-, OnCollision-**

- Collider를 가진 두 오브젝트가 만나 발생하는 충돌 관련 함수입니다.

### 오브젝트에 스크립트 적용 방법

드래그 앤 드롭으로 스크립트 파일을 오브젝트에 적용할 수 있습니다.

![0%2058df47aa2ad2467d844cea7367a5d8e0/Untitled.png](0%2058df47aa2ad2467d844cea7367a5d8e0/Untitled.png)

## 클래스 접근지정자

- 자바나 c#에서 클래스 내에서 멤버의 접근을 제한하는 역할
- public > protected > default > private 순으로 허용도가 감소
- public : 해당 클래스가 어떤 접근을 하든 모두 허용됩니다.
- protected : 상속받은 클래스 또는 같은 패키지에서만 접근이 가능합니다.
- default : 기본제한자로써, 자신 클래스 내부와 같은 패키지 내에서만 접근이 가능합니다.
- private : 외부에서 접근이 불가능하고, 같은 클래스 내부에서만 접근이 허용됩니다.

## **c# 스크립트를 이용한 게임 예시**

### 리듬코딩

- 프로젝트 설명 : 리듬게임과 코딩을 합쳐 재밌게 코딩을 공부할 수 있는 게임. (PC)**경북대학교 코드페어(19.11.20) 최우수상 수상**
- 팀원 : 윤치호(메인코딩), 장우진(서브코딩,디자인), 박지환(기획)
- 관련사진

![0%2058df47aa2ad2467d844cea7367a5d8e0/Untitled%201.png](0%2058df47aa2ad2467d844cea7367a5d8e0/Untitled%201.png)

![0%2058df47aa2ad2467d844cea7367a5d8e0/Untitled%202.png](0%2058df47aa2ad2467d844cea7367a5d8e0/Untitled%202.png)

![0%2058df47aa2ad2467d844cea7367a5d8e0/Untitled%203.png](0%2058df47aa2ad2467d844cea7367a5d8e0/Untitled%203.png)

게임 실행 영상

[https://www.youtube.com/watch?v=sYgiWUvvGiQ](https://www.youtube.com/watch?v=sYgiWUvvGiQ)

**게임 다운로드 파일**

[리듬코딩 테스트 게임파일](https://drive.google.com/open?id=1E8oATU0Po_ta1jFRJpBQUY008hC8idfq)

### 주요 사용 기능들

- c# 스크립트를 이용한 리듬게임의 노트생성 구현
- 유니티 에디터를 활용하여 변수 및 이미지 관리
- Time.deltaTime을 이용한 노트 딜레이 설정
- 자체 좌표계 이용한 높이에 따른 판정 시스템 구현
- UI 버튼 기능을 이용한 전체적인 UI배치
- 점수 변수 관리를 통한 전체 기록 관리 및 표시

### **c#스크립트 배우기**

 이제 게임을 직접 만들어보며 c# 스크립트에 대해 알아봅시다. 

 최대한 유니티 편집기의 기능을 사용하지 않고 c# 스크립트를 사용하여 테트리스 게임을 만들어 보겠습니다.