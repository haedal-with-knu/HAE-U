# OT

## 수업내용

- 유니티 설치하기
- 기본 환경설정
    - 빌드 가능 플랫폼들
    - 비주얼 스튜디오 자동완성 기능
    - 유니티 화면 구성
    - 오브젝트 관리 단축키
- 추가기능 관리하기
    - 어셋 스토어 이용하기
    - 패키지 매니저 이용하기

# **유니티 설치하기**

[https://unity3d.com/kr/get-unity/download](https://unity3d.com/kr/get-unity/download) - 다운로드 링크

유니티 '허브' 다운로드

![https://user-images.githubusercontent.com/48755297/87240425-7bb55600-c454-11ea-8766-09502f5a6b8f.png](https://user-images.githubusercontent.com/48755297/87240425-7bb55600-c454-11ea-8766-09502f5a6b8f.png)

로그인 하여 라이선스 인증해줍니다.

(아이디가 없을 경우 유니티 홈페이지 or 유니티 허브에서 회원가입 가능합니다)

![https://user-images.githubusercontent.com/48755297/87240459-c3d47880-c454-11ea-85ff-fd28facd924f.png](https://user-images.githubusercontent.com/48755297/87240459-c3d47880-c454-11ea-85ff-fd28facd924f.png)

![https://user-images.githubusercontent.com/48755297/87240472-d51d8500-c454-11ea-8a80-05d40bf22a27.png](https://user-images.githubusercontent.com/48755297/87240472-d51d8500-c454-11ea-8a80-05d40bf22a27.png)

![https://user-images.githubusercontent.com/48755297/87240489-fbdbbb80-c454-11ea-9c93-a0cf6107d876.png](https://user-images.githubusercontent.com/48755297/87240489-fbdbbb80-c454-11ea-9c93-a0cf6107d876.png)

![https://user-images.githubusercontent.com/48755297/87240547-5b39cb80-c455-11ea-9ac9-d72ae0ace056.png](https://user-images.githubusercontent.com/48755297/87240547-5b39cb80-c455-11ea-9ac9-d72ae0ace056.png)

유니티 다운로드 링크(4.2f)[https://unity3d.com/get-unity/download/archive](https://unity3d.com/get-unity/download/archive)

![https://user-images.githubusercontent.com/48755297/87240576-95a36880-c455-11ea-86e9-14b4ffb5da37.png](https://user-images.githubusercontent.com/48755297/87240576-95a36880-c455-11ea-86e9-14b4ffb5da37.png)

Microsoft Visual Studio Android Build Support iOS Build Support

![https://user-images.githubusercontent.com/48755297/87242658-bf668a80-c469-11ea-993e-a9033999da2a.png](https://user-images.githubusercontent.com/48755297/87242658-bf668a80-c469-11ea-993e-a9033999da2a.png)

![https://user-images.githubusercontent.com/48755297/87242707-094f7080-c46a-11ea-8d0b-3a5e3058b757.png](https://user-images.githubusercontent.com/48755297/87242707-094f7080-c46a-11ea-8d0b-3a5e3058b757.png)

![https://user-images.githubusercontent.com/48755297/87242744-69461700-c46a-11ea-977e-a993290f32f7.png](https://user-images.githubusercontent.com/48755297/87242744-69461700-c46a-11ea-977e-a993290f32f7.png)

# **기본 환경설정**

## 빌드 가능 플랫폼들

빌드 하고자하는 플랫폼 설정 (File -> Build Setting , 단축키 : ctrl+shift+B)

![https://user-images.githubusercontent.com/48755297/87275590-67875c80-c519-11ea-8b39-d01094a81c82.png](https://user-images.githubusercontent.com/48755297/87275590-67875c80-c519-11ea-8b39-d01094a81c82.png)

## 비주얼 스튜디오 자동완성기능 적용

![https://user-images.githubusercontent.com/48755297/87275959-3fe4c400-c51a-11ea-9726-3a236a15e280.png](https://user-images.githubusercontent.com/48755297/87275959-3fe4c400-c51a-11ea-9726-3a236a15e280.png)

- 시작-실행-appwiz.cpl 입력 (또는 '프로그램 추가/제거' 찾아서 실행)
- 'Microsoft Visual Studio Installer' 를 찾아서 마우스 오른쪽 클릭 - 변경
- Visual Studio '수정' 클릭
- 오른쪽에서 'Unity를 사용한 게임 개발' 항목을 확장하고 'Unity 2017.2 64비트 편집기' 체크
- (여기까지만 하고 '수정' 버튼을 눌러 나온 뒤 유니티와 VS를 다시 켜면 나의 경우 인텔리센스가 동작했다)
- 혹시 모르니 '개별 구성 요소' 탭 - 코드 도구 - 'NuGet 패키지 관리자' 체크가 안되어있으면 체크
- '수정' 버튼 누르고 체크한 것들이 추가로 설치될때까지 대기
- 이제 유니티, VS를 켜면 자동완성이 됨

![https://user-images.githubusercontent.com/48755297/87276067-89cdaa00-c51a-11ea-8898-e86a320cfe07.png](https://user-images.githubusercontent.com/48755297/87276067-89cdaa00-c51a-11ea-8898-e86a320cfe07.png)

![https://user-images.githubusercontent.com/48755297/87276091-93efa880-c51a-11ea-9b4b-1615e8a6cda3.png](https://user-images.githubusercontent.com/48755297/87276091-93efa880-c51a-11ea-9b4b-1615e8a6cda3.png)

![https://user-images.githubusercontent.com/48755297/87276100-98b45c80-c51a-11ea-919d-0890c0d707d7.png](https://user-images.githubusercontent.com/48755297/87276100-98b45c80-c51a-11ea-919d-0890c0d707d7.png)

![https://user-images.githubusercontent.com/48755297/87276102-9b16b680-c51a-11ea-8a6c-e9e241c9a2ad.png](https://user-images.githubusercontent.com/48755297/87276102-9b16b680-c51a-11ea-8a6c-e9e241c9a2ad.png)

## 유니티 화면 구성

 유니티를 처음 실행했을때 실행되는 화면입니다. 구성요소를 하나씩 알아가보겠습니다.

![OT%20843e60fa03834cfe9fd2c3738d33b5de/Untitled.png](OT%20843e60fa03834cfe9fd2c3738d33b5de/Untitled.png)

### Inspector창

 Inspect는 관찰한다는 뜻으로 이 창은 게임 오브젝트를 관찰하는 역할을 맡고 있습니다. 게임 오브젝트들의 기능들을 다 볼 수 있으며 이를 조정할 수 있습니다.

![OT%20843e60fa03834cfe9fd2c3738d33b5de/Untitled%201.png](OT%20843e60fa03834cfe9fd2c3738d33b5de/Untitled%201.png)

### Project 창

 Project 창은 유니티 전용 파일 탐색기입니다. 여기서 사용할 파일들을 보고 관리할 수 있습니다. 단, Project 창에선 파일들의 확장자가 보이지 않는다는 점을 주의해야 합니다.

![OT%20843e60fa03834cfe9fd2c3738d33b5de/Untitled%202.png](OT%20843e60fa03834cfe9fd2c3738d33b5de/Untitled%202.png)

### Console 창

 Console 창은 프로젝트 옆의 탭을 눌러서 들어갈 수 있습니다. 유니티의 메시지를 이 콘솔 창을 통하여 볼 수 있습니다. 주로 디버깅용으로 사용합니다.

![OT%20843e60fa03834cfe9fd2c3738d33b5de/Untitled%203.png](OT%20843e60fa03834cfe9fd2c3738d33b5de/Untitled%203.png)

### Hierarchy 창

 Hierarchy는 계층이라는 뜻으로 hierarchy에선 게임 오브젝트들의 부모- 자식 관계를 볼 수 있고 Scene의 게임 오브젝트들을 관리할 수 있습니다.

![OT%20843e60fa03834cfe9fd2c3738d33b5de/Untitled%204.png](OT%20843e60fa03834cfe9fd2c3738d33b5de/Untitled%204.png)

### Scene 창

 현재 구성하고 있는 장면을 보여주는 창입니다. 여기에 오브젝트들을 배치하여 관리할 수 있습니다.

![OT%20843e60fa03834cfe9fd2c3738d33b5de/Untitled%205.png](OT%20843e60fa03834cfe9fd2c3738d33b5de/Untitled%205.png)

### Game 창

 Scene에서 배치한 오브젝트들을 카메라가 비추고 있는 장면을 볼 수 있습니다.

![OT%20843e60fa03834cfe9fd2c3738d33b5de/Untitled%206.png](OT%20843e60fa03834cfe9fd2c3738d33b5de/Untitled%206.png)

## 오브젝트 관리 단축키

### 간단한 단축키들

Q : 화면 이동

W : X, Y축 이동

![https://user-images.githubusercontent.com/48755297/87397749-c7e8cd80-c5ef-11ea-91c5-240eb6be9159.png](https://user-images.githubusercontent.com/48755297/87397749-c7e8cd80-c5ef-11ea-91c5-240eb6be9159.png)

E : 오브젝트 회전

![https://user-images.githubusercontent.com/48755297/87397788-da630700-c5ef-11ea-96b0-940835ef9552.png](https://user-images.githubusercontent.com/48755297/87397788-da630700-c5ef-11ea-96b0-940835ef9552.png)

R : X, Y축으로 크기 조정

![https://user-images.githubusercontent.com/48755297/87397857-f797d580-c5ef-11ea-9cf7-574ead74c664.png](https://user-images.githubusercontent.com/48755297/87397857-f797d580-c5ef-11ea-9cf7-574ead74c664.png)