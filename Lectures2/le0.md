# 플랫폼 게임 만들기 0

## 수업내용

- 플랫폼 게임 시작하기
    - 플랫폼 게임이란
    - 물리 엔진이란
    - 플랫폼 게임의 예시

# 플랫폼 게임 시작하기

## 플랫폼 게임이란

### 플랫폼 게임

 **플랫폼** 이란 발판을 의미합니다. 따라서 플랫포머 게임이란 발판이 등장하는 게임을 뜻합니다. 어떤 장르와 결합되었든 기본적으로 액션장르의 하위 부류입니다.

 구체적으로는, 플레이어가 캐릭터를 조종할 때 **발판 위를 뛰어다니는 점프 컨트롤**이 중요한 게임 장르를 의미합니다. 국내에서는 플랫포머 장르명이 많이 쓰이지 않고 '횡스크롤 액션 게임'이나 '사이드뷰 런앤건 게임' 등등과 같이 다른 명칭으로 불리는 경우가 많습니다. 그래도 엄연히 플랫포머 게임이 가지는 성격과 공통점이 존재합니다.

(출처 : 나무위키)

## 물리 엔진이란

### **물리엔진**

- 오브젝트를 물리 동작에 맞춰 움직임을 구현하는 시뮬레이션용 라이브러리 오브젝트의 질량, 마찰 계수, 중력 등을 고려해 움직임을 자동으로 계산 -> 사실적인 동작을 쉽게 구현할 수 있습니다.

### **스크립트 vs Physics**

**스크립트로 제어**

- 복잡하고 관련된 코딩능력(C#) 필요, 비자연스러운 움직임

    ![https://user-images.githubusercontent.com/48755297/87005346-d2732380-c1f9-11ea-89b8-8f6aed766e1a.jpg](https://user-images.githubusercontent.com/48755297/87005346-d2732380-c1f9-11ea-89b8-8f6aed766e1a.jpg)

**Physics로 제어**

- 상대적으로 짧고 간단한 코딩, 자연스러운 움직임, 유니티의 다른 기능들과 최적화

    ![https://user-images.githubusercontent.com/48755297/87005446-f8002d00-c1f9-11ea-8b89-cacf2a725ef8.png](https://user-images.githubusercontent.com/48755297/87005446-f8002d00-c1f9-11ea-8b89-cacf2a725ef8.png)

## 플랫폼 게임의 예시

### 업사이드다운

 현재 안드로이드 마켓에 퍼블리싱 준비중인 플랫폼게임

![https://github.com/haedal-with-knu/HAE-U/raw/master/Readme/ud1.png](https://github.com/haedal-with-knu/HAE-U/raw/master/Readme/ud1.png)

- 프로젝트 설명 : 중력을 바꾸어가며 스테이지들을 클리어해나가는 플랫폼 게임 (Android)
- 팀원 : 윤치호, 장우진(캐릭터 디자인)
- 게임 실행 영상([https://www.youtube.com/watch?v=NZiZURiTpno](https://www.youtube.com/watch?v=NZiZURiTpno))
- 게임 다운로드 링크(테스트버전)([https://play.google.com/store/apps/details?id=com.CHHO.UPSIDEDOWN](https://play.google.com/store/apps/details?id=com.CHHO.UPSIDEDOWN))
- 관련사진.

![https://github.com/haedal-with-knu/HAE-U/raw/master/Readme/ud2.PNG](https://github.com/haedal-with-knu/HAE-U/raw/master/Readme/ud2.PNG)

![https://github.com/haedal-with-knu/HAE-U/raw/master/Readme/ud3.PNG](https://github.com/haedal-with-knu/HAE-U/raw/master/Readme/ud3.PNG)

### 주요 사용 기능들

- physics 2D를 이용한 중력 구현 및 활용
- c# 스크립트를 이용한 캐릭터 움직임 관리
- 유니티 에디터를 활용하여 변수 및 이미지 관리
- 파티클을 사용한 이펙트 효과 추가
- 오브젝트에 Light 기능 추가하기
- RayCast기능을 이용한 바닥 충돌 확인
- UI 버튼 기능을 이용한 전체적인 UI 배치
- 점수 변수 관리를 통한 전체 기록 관리 및 표시
- 안드로이드 마켓 연동 및 스코어보드 사용