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

## ThreadTest클래스에 코드 수정하기
```java
public class MyThread extends Thread{

	@Override
	public void run() {
		//프로세스의 독립적인 수행을 위한 영역
		for (int i = 0; i < 10; i++) {
			System.out.println("스레드 진행 중"+i);
		}
	}
}
```

## RunnableTest클래스 코드 수정하기
```java
public class MyThread2 implements Runnable{
	@Override
	public void run() {
		//프로세스의 독립적인 수행을 위한 영역
		for (int i = 0; i < 10; i++) {
			System.out.println("러너블 진행중"+i);
		}
	}
}
```

## ThreadMain클래스에 코드 추가하기
```java
public class ThreadMain {
	public static void main(String[] args) {
		
		MyThread t = new MyThread();
		t.start();//run()메서드를 호출하는 메서드
		//t.run();은 run()메서드를 독립적으로 수행하지 못한다.
		//즉, 일반 메서드처럼 호출해버림.
		//run()메서드의 내용을 별개로 수행하고 싶다면
		//t.start()를 이용해야 함.

		MyThread2 th2 = new MyThread();
		Thread t = new Thread(th2);
		t.start();
		
		for(int I = 0; i< 10; I++) {
			System.out.println("메인함수 실행중" + I);
		}
	}
}
```

## 익명클래스를 람다식으로 표현하기
- Runnable인터페이스를 상속해 구현하지 않고, 익명클래스로 만들어서 사용한다.
```java
package test;

public class Test {
	public static void main(String[] args) {
		//Runnable 인터페이스를 익명 객체로 처리
		Runnable white = () -> {
			while(true) {
				System.out.println("백기 올");
			}
		};
		
		Thread whiteFlag = new Thread(white);
		whiteFlag.start();
		
	}
}
```

## 스레드의 이름,상태,순위

## ThreadName 클래스 생성
```java
public class ThreadName extends Thread {
	@Override	
	public void run() {
		this.setName("Thread3");
		System.out.println("현재실행되고있는스레드의이름: Thread.currentThread().getName());
	System.out.println("현재실행되고있는스레드의상태: Thread.currentThread().getState());
	System.out.println("현재실행되고있는스레드의우선순위: Thread.currentThread().getPriority);
	}
}
```

## MainThread클래스 생성
```java
public static void main(String [] args) {

	ThreadName tn = new ThreadName();
	tn.start();

	System.out.println("현재실행되고있는스레드의이름: Thread.currentThread().getName());
	System.out.println("현재실행되고있는스레드의상태: Thread.currentThread().getState());
	System.out.println("현재실행되고있는스레드의우선순위: Thread.currentThread().getPriority);
}
```

## 스레드 상태
- 스레드는 생성하고 실행, 종료되기까지 다양한 상태를 가진다.
- 각 스레드의 상태는 스레드 클래스에 정의되어 있으며, Thread.State 타입으로 알 수 있다.
- 스레드 상태에 따라 6개의 타입으로 분류하고 있다.

|상태|상수|설명|
|---|----|---|
|생성|NEW|스레드 객체가 생성되었지만 아직 start()메서드가 호출되지 않은 상태|
|대기|RUNNABLE|실행 대기 또는 실행 상태로 언제든지 갈 수 있는 상태|
|일시정지|WATING<br>TIMED_WATING<br>BLOCKED|다른 스레드가 종료될 때까지 대기하는 상태<br>주어진 시간동안 대기하는 상태<br>락이 풀릴 때까지 대기하는 상태|
|종료|TERMINATED|수행을 종료한 상태|

## 1. New와 RUNNABLE,TERMINATED
- 처음 스레드가 생성되면 스레드는 NEW 상태가 된다.
- 생성 이후에 start() 메서드를 실행하면 스레드는 RUNNBLE 상태로 변하고
- 시작 이후에 스레드가 조욜되면 TERMINATED상태가 된다.

## 2.WAIT
- 스레드 WAIT 상태는 필요에 의해서 스레드를 잠시 멈춤 상태로 두는 것
- 스레드를 잠시 멈춤 상토래 만들 때는 일정 시간을 지정하거나, 멈춤 상태의 락이 풀릴 때까지 대기하도록 만들 수 있다.

## 상태변화 메서드
- 스레드의 상태를 변화시키는 다양한 메서드에 대해서 알아보자

## sleep()메서드
- sleep(int mils)메서드는 주어진 시간 동안 스레드를 정지시키는 메서드이다.
- 해당 기능은 모든 스레드를 대기시켜주며, 주어진 시간이 지나면 풀리게 된다.

### SleepThread클래스 생성
```java
public class SleepThread extends Thread{
	public void run() {
		System.out.println("카운트다운 5초");
		for(int I = 5; i>=0; I--) {
			if(i!=0) {
				try{
					Thread.sleep(1000);//1000당 1초
				} catch(Exception e) {

				}//catch
			}//if
		}//for
		System.out.println("종료!");
	}
}
```
### SleepMain 클래스 생성
```java
public class SleepMain{
	public static void main(String[] args) {
		SleepThread st = new SleepThread();
		st.start();
	}
}
```

## wait()와 notify()
- 여러 개의 스레드가 동시에 동작하다 보면, 하나의 스레드가 완료되어야 다음 스레드가 동작할 수 있는 경우가 있다.
- 예를 들어 한쪽에서는 물건을 나르고, 다른 한쪽에서는 물건을 쌓는 스레드가 있다고 가정해보자.
- 만약 쌓을 물건이 없다면 물건을 나르는 스레드는 할일이 없어진다.
- 이때, 물건을 나르는 스레드를 잠시 중지시키고, 물건이 오면 다시 나르도록 할 수 있다.
- wait()메서드는 스레드를 대기시키고, notify()메서드는 대기중인 스레드를 다시 동작시킬 때 사용한다.


### Storage클래스
```java
package test;

public class Storage {
	private int stackCount = 10;
	public synchronized void addStack(int stackCount) {
		this.stackCount += stackCount;
		if(this.stackCount >= 10) {
			System.out.println("== 스레드 깨우기 ===");
			notify();
		}
	}
	
	public synchronized void popStack(int leaveCount) {
		try {
			if(leaveCount > this.stackCount) {
				this.stackCount = 0;
			} else {
				this.stackCount -= leaveCount;
			}
			
			if(this.stackCount == 0) {
				System.out.println("== 짐 없음 대기 ===");
				wait();
				System.out.println("==짐 없음 대기완료===");
			}
		} catch (Exception e) {
			// TODO: handle exception
		}
	}
	
	public int getStackCount() {
		return this.stackCount;
	}
}
```

### ThreadWaitExample클래스
```java
package test;

class AddStackThread extends Thread{
	private Storage stroage;
	public AddStackThread(Storage storage) {
		this.stroage = storage;
	}
	
	@Override
	public void run() {
		try {
			while(true) {
				Thread.sleep(1000);
				if(this.stroage.getStackCount() == 0) {
					System.out.println("짐 10개 추기");
					this.stroage.addStack(10);
				}
			}
		} catch (Exception e) {
			// TODO: handle exception
		}
	}
}

class PopStackThread extends Thread{
	private Storage storage;
	public PopStackThread(Storage storage) {
		this.storage = storage;
	}
	
	@Override
	public void run() {
		try {
			while(true) {
				Thread.sleep(1000);
				System.out.println("짐 5개 나르기");
				this.storage.popStack(5);
			}
		} catch (Exception e) {
			// TODO: handle exception
		}
	}
}


public class ThreadWaitExample {
	public static void main(String[] args) {
		Storage s = new Storage();
		AddStackThread add = new AddStackThread(s);
		PopStackThread pop = new PopStackThread(s);
		
		add.start();
		pop.start();
	}
	
	
}
```






