# 스레드
- 우리는 컴퓨터로 문서를 작성하면서 동시에 음악을 듣고, 메신저를 사용할 수 있다.
- 이처럼 동시에 두 가지 이상의 작업을 처리하는 것을 '멀티태스킹'이라고 한다.
- 컴퓨터는 어떻게 여러 가지 작업을 동시에 할 수 있을까?
- 컴퓨터에는 멀티태스킹을 위해 '프로세스'와 '스레드'라는 두 가지 도구가 있다.

## 프로세스
- 컴퓨터에 저장되어 있는 파일을 실행하는 순간 메모리에 올라가고 동작하게 되는데 이 상태를 프로세스 라고 한다.
- 프로세스는 독립적으로 메모리에 등록되므로 여러 개의 프로그램을 동시에 실행할 수 있다.

## 스레드
- 프로스세 내부에 존재하면서 실행 흐름을 나타내는 것

## 프로세스가 실행되는 방식
1. 시간 분할 방식 : 모든 프로세스에게 동일한 시간을 할당하고 골고루 실행되는 방식
2. 선점형 방식 : 각각의 프로세스에게 우선 순위를 부여하고 높은 순으로 실행되는 방식


## jvm이 스레드 처리시 하는 일
- 스레드 스케쥴링
- 스레드가 몇 개 존재하는지
- 스레드가 실행되는 프로그램 코드의 메모리 위치가 어딘지
- 현재 스레드의 상태는 무엇인지
- 스레드의 우선순위는 몇인지

## 개발자가 스레드 처리시 하는 일
- 자바 스레드로 작동할 작업이 무엇인지 코드로 작성
- 스레드 코드가 실행할 수 있도록 JVM한테 요청

## 스레드의 생성
- 스레드를 생성하는 방법에는 두 가지가 있다.

### ThreadTest클래스
```java
public calss ThreadTest extends Thread{
	public void run() { //run()메서드 오버라이딩
		//작업할 내용
	}
}
```

### RunnableTest클래스
```java
public calss RunnableTest implements Runnable{
	public void run() { //run()메서드 오버라이딩 필수!
		//작업할 내용
	}
}
```

### ThreadMain
```java
public class ThreadMain{
    public static void main(String[]args){
	ThreadTest t1 = new ThreadTest(); //객체생성
	t1.start();

	러너블 인터페이스 구현시 스레드 코드가 실행할 수 있도록 JVM에 요청
	ThreadTest t2 = new ThreadTest(); //객체 생성
	Thread t = new Thread(t2);
	t.start();
  }
```



















