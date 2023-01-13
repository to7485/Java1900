# 실습 환경 구축하기

## 내 PC에 실습을 위한 폴더 만들기
내 PC -> D드라이브 진입 -> JAVA1900_이니셜 -> 안에 util,work 폴더만들기

![image](https://user-images.githubusercontent.com/54658614/211975967-b510f6c6-1f98-4372-b52c-65c6ed39bb6e.png)

<hr>


## 자바 설치하기
- [JDK다운로드](https://www.oracle.com/java/technologies/downloads)

### 자바의 버전을 보면 많다 어떤 버전을 사용하는것이 좋은가??
기업에서 이미 운영하고 있는 프로젝트들이 있을 것이다. 대부분 Java8버전으로 하는 경우가 많다.
프로젝트를 새로 시작하는 경우 Java11, Java17을 사용하는 4경우가 있다.

### 특정 자바 버전을 학습 해야 할까???
12,17과 같은 특정 Java버전만을 "학습"할 필요가 없다.
자바는 하위호환성이 매우 높기 때문이다.
<hr>

## 통합 개발환경
통합 개발 환경(統合開發環境, Integrated Development Environment, IDE)은 코딩, 디버그, 컴파일, 배포 등 프로그램 개발에 관련된 모든 작업을 하나의 프로그램 안에서 처리하는 환경을 제공하는 소프트웨어이다.

### 대중적인 IDE
- 이클립스(Eclipse) : 웹, Java, C, C++
- Visual Studio : C, C++, C#, Python
- Intellij : Java, C/C++
등등 많은 IDE가 있다.

## 이클립스 설치하기
- [Eclipse다운로드](https://www.eclipse.org/)
<hr>

## 자바란?
썬 마이크로시스템즈 소속 제임스고슬링 등의 일부 연구진들은 '그린프로젝트'라는 이름으로 '오크(Oak)'라는 언어를 개발하고 있었다.<br>오크는 오디오,tv,세탁기 등 각각의 가전제품을 제어하는 통합된 언어로써 개발중이었지만 결국 목적을 달성하지 못하고 실패로 돌아간다.<br>그 무렵 웹(www)이 급속도로 발전하게 되고, 이에 발맞추고자 썬에서는 오크의 명칭을 Java로 바꾼뒤 서로 다른 컴퓨터(OS - 운영체제)사이에서 호환성과 이식률을 높인 언어로 발전시켰다.

![image](https://user-images.githubusercontent.com/54658614/211973993-8e9d86f8-5251-48b8-9e10-4567dde3ef49.png)

<hr>

## 자바가 잘 설치되어있는지 확인하는법

win + r -> 실행창에 cmd -> java -verion 입력

![image](https://user-images.githubusercontent.com/54658614/211975334-e2287139-5269-4218-8dd0-1167fd62eea4.png)

```diff
- ※ jdk를 먼저 설치하지 않으면 이클립스가 실행되지 않습니다!!
```

<hr>

## 이클립스 실행해보기
이클립스를 켜고 Browse를 눌러 우리가 만들어 놓은 work 폴더로 경로를 잡아주자.(앞으로 우리가 작업하는 프로젝트들은 work폴더에 저장될 것이다.)

![image](https://user-images.githubusercontent.com/54658614/211976280-0159d649-c5d5-47c3-840a-09f4e37d4e24.png)

<hr>

## 이클립스 프로그램 구성

![image](https://user-images.githubusercontent.com/54658614/212237771-1da23aee-2b7b-4d49-9692-e1b87980a835.png)

## 자바 프로젝트의 구성
자바는 패키지라고 하는 폴더 단위로 프로젝트를 관리한다.<br>
내가 손흥민이 최근에 넣었던 골에 대한 영상을 찾고 싶은데 하나의 폴더에 축구 동영상 50개와 야구 동영상 50개가 있다면 1/100 확률로 찾을 수 있다.
하지만 최소한 축구 동영상 폴더와 야구 동영상 폴더를 나눠서 관리를 하게 되면 1/50 확률로 찾을 수 있는 속도가 2배 증가한다.

## 자바 프로젝트 생성하기
![image](https://user-images.githubusercontent.com/54658614/212238723-e89acb35-1605-4a1b-8e9f-716fd097cc81.png)

![image](https://user-images.githubusercontent.com/54658614/212238789-2ef70972-6e66-432e-9380-159f46f01526.png)

![image](https://user-images.githubusercontent.com/54658614/212238858-e61b8d78-c9a4-45ee-9480-ad523f1589ad.png)

![image](https://user-images.githubusercontent.com/54658614/212238952-7869b3bd-a2ea-4eeb-a94a-5081bedc8ecc.png)

## 폴더에 해당하는 패키지 생성하기

![image](https://user-images.githubusercontent.com/54658614/212239071-7dea18ab-2129-470a-b383-ae8a81c6a9d6.png)

### 패키지 이름을 적고 finish를 누릅니다.

![image](https://user-images.githubusercontent.com/54658614/212239347-bc640c8d-266a-4e4a-b1cf-6ca13aad557b.png)

### 그러면 비어있는 패키지가 생성되게 됩니다.

![image](https://user-images.githubusercontent.com/54658614/212239455-3f18af92-83b4-4f2f-8c43-276e56506204.png)

## 코드를 작성하는 공간인 클래스 생성하기

![image](https://user-images.githubusercontent.com/54658614/212239571-0380fc1a-b15c-4f17-aacd-036e5e6d9b05.png)

### 클래스를 작성할 때 클래스의 이름의 첫번째 글자는 반드시 대문자로 작성해야 합니다.

![image](https://user-images.githubusercontent.com/54658614/212239611-d741c393-40b5-430b-8b43-3b8e62956724.png)

![image](https://user-images.githubusercontent.com/54658614/212239789-91e1818d-fb55-4fba-83b5-c727a4cbae4c.png)

### 클래스를 작성하면 항상 main이라고 하는걸 작성해주자 지금 당장은 뭔지 모르겠지만 자바가 실행될 때 main 영역 안에 있는 코드가 실행된다.

![image](https://user-images.githubusercontent.com/54658614/212240409-43e3b09e-921c-43cc-8c1b-74e1859e45cf.png)





