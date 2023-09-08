# 예외 처리
## 에러(error)와 예외(exception)
- 자바 프로그램을 실행하다 보면 갑자기 프로그램이 종료되거나, 어떤 원인에 의해 잘못 동작하여 오류 메세지가 나타나는 등 예기치 못한 오류가 발생한다.
- 전자는 우리가 해결할 수 없는 시스템에 에러가 발생해 프로그램이 종료된 경우이며 후자는 프로그램 사용 중 발생한 오류를 개발자가 처리해 메세지가 출력된 경우이다.

## 에러(error)
- 에러는 시스템에 비정상적인 상황이 생겼을 때 발생한다.
- 외부 요인일 수도 있고, 프로그램 구동 중에 발생하는 치명적인 오류일 수도 있다.
- 이러한 에러들은 개발자가 예측하거나 처리할 수 없는 영역이다.

|에러의 종류| 상황 |
|-----------|-------|
|OutOfMemoryError|프로그램 실행 중 메모리 부족|
|IOError|입출력 에러|
|StackOverFlowError|가용 메모리 부족 현상, 재귀 호출 문제시 발생|

## 예외(exception)
- 예외란 대체로 프로그램 구동 중에 나타나는 오류들을 말한다.
- 문법적으로는 문제가 없어보이지만 실제 운영 중에 생기는 문제들이다.
- 예외는 체크 예외(checked exception)와 비체크 예외(uncheked exception)두 가지가 있다.
### 체크 예외
- 자바 소스를 컴파일 하는 과정에서 검사한다.
- 보통 문법적으로 강제하여 예외 처리를 해야 하는 경우
### 비체크 예외
- 컴파일 과정에서 검사하지 않으므로 사용자의 경험이나 테스트로 찾아야 하는 경우

|구분|체크 예외|비체크 예외|
|---|----------|------------|
|처리 여부|문법적으로 예외 처리를 강제함<br>반드시 처리 해야 함|문법적으로 강제하지 않음<br>개발자의 판단에 의해 처리|
|확인 시점| 컴파일 단계| 실행 단계|
|예외 클래스|Runtime Exception을 제외한 모든 예외<br>IOException<br>SQLException등|Runtime Exception의 자식 클래스 모두 포함<br>NullPointerException<br>IndexOutOfBoundsException<br>ClassNotFoundException|

## 제네릭스
### 제네릭스란?
- 일반적인 코드를 작성하고 이 코드를 다양한 타입의 객체에 대하여 재사용하는 객체 지향 기법이다.
- 객체의 타입을 컴파일 할 때 체크하기 때문에 객체의 타입에 대해 안정성을 높히고 형변환을 하는 번거로움을 줄일 수 있다.

ex1_generic 패키지 생성
#### GenEx 클래스 정의
우선 GenEx클래스를 만든후 <T>를 추가해야 한다. 클래스 이름을 정하는 과정에서는 <T>가 안들어간다.<br>
```java
public class GenEx<T>{
  //public class 클래스명<T>{}
  //public interface 인터페이스명<T>{}
  //T를 타입변수(type variable)이라 하며 Type의 첫글자에서 따온것이다.
  //다른 글자를 사용해도 되는데 E(Element),K(key),V(Value)를 많이 사용한다.
	T value;

	public T getValue() {
		return value;
	}

	public void setValue(T value) {
		this.value = value;
	}
}
```
#### GenEx_Main클래스 정의
```java
public class GenEx_Main {
	public static void main(String[] args) {
		// 사용자가 원하는 형태로 객체 생성
		GenEx<String> v1 = new GenEx<String>(); //T자리에 실제 타입을 지정한다.
		v1.setValue("100");

		System.out.println(v1.getValue());

		// 정수를 가지는 GenEx객체를 생성하자!
		// 제네릭 타입은 기본자료형을 인식하지 않음
		// 따라서 int, double등의 기본자료형을 제네릭타입으로 이용하고자 할 때는
		// Integer, Double등의 클래스를 이용해야 한다. 
  
		GenEx<Integer> v2 = new GenEx<Integer>();
		v2.setValue(1000);
		System.out.println(v2.getValue()+10);

		GenEx<Character> v3 = new GenEx<Character>();
		v3.setValue(‘A’);
		System.out.println(v3.getValue());

		GenEx<Double> v4 = new GenEx<Double>();
		v4.setValue(3.14);
		System.out.println(v4.getValue());
	}
}
```
### 멀티타입 파라미터
타입은 두개 이상의 멀티 타입 파라미터를 사용할 수 있고 이 경우 각 타입 파라미터를 콤마로 구분합니다<br>
```java
class People<T,M>{
    private T name;
    private M age;
	
    People(T name, M age){
        this.name = name;
        this.age = age;
    }

    public T getName() {
        return name;
    }
    public void setName(T name) {
        this.name = name;
    }
    public M getAge() {
        return age;
    }
    public void setAge(M age) {
        this.age = age;
    }
  }
```
#### ExGeneric 클래스 생성
```java
public class ExGeneric {
    public static void main(String []args){
        //타입 파라미터 지정
        People<String,Integer> p1 = new People<String,Integer>("Jack",20);
        //타입 파라미터 추정
        People<String,Integer> p2 = new People("Steve",30);
  
        System.out.println(p1.getName());
        System.out.println(p1.getAge());
        System.out.println("------------------");
        System.out.println(p2.getName());
        System.out.println(p2.getAge());
        System.out.println("------------------");
    }
} 
```
### 제네릭 메서드
- 메서드의 선언부에 지네릭 타입이 선언된 메서드를 제네릭 메서드라고 한다.
- 선언 위치는 반환 타입 바로 앞이다.

```java
public <T> void 메서드명(클래스명<T> 객체명)
```

 위 사람의 정보를 저장하는 코드에서 객체들의 이름이 일치하면 true, 다르면 false<br>
 나이가 일치하면 true, 다르면 false를 받아 논리연산하는 함수 만들기<br>
 ```java
   public static<T,V> boolean compare(People<T,V>p1, People<T,V>p2) {
      boolean nameCompare = p1.getName().equals(p2.getName());
      boolean ageCompare =p1.getAge().equals(p2.getAge());
      return nameCompare && ageCompare;
  } 
 ```

#### 문제로 내도 되고 같이 풀어도됨
Gen클래스를 만들어 제네릭 타입T를 갖는 printArr메서드를 생성한다.<br>
printArr메서드 내부에서 배열을 순차적으로 보여줄수 있게 하는 코드를 작성.<br>

Main클래스를 만들어 Integer[], Double[], Character[]을 각각 만든 뒤<br>
Gen클래스의 printArr메서드를 각각 호출하여 배열의 내용을 출력하도록 해보자.<br>

결과 :<br>
 1 2 3 4 5  //정수배열 출력<br>
 1.1 2.2 3.3 4.4 5.5 //실수배열 출력<br>
 A B C D E //문자배열 출력<br>
  
#### Gen클래스 정의
아래의 초록색 <T>는 둘 중에 한 개만 넣어주면 되지만,<br>
메서드에서 제네릭 타입을 사용할 경우 메서드쪽에 넣어주는 것이 더 좋다.<br>
```java
public class Gen <T> {
	public <T> void printArr(T[] arr){

		for(int i = 0; i < arr.length; i++){
			System.out.print(" " + arr[i]);
		}
		System.out.println();
	}
}
```  
#### GenEx클래스 정의
```java
public class GenEx{
	public static void main(String[] args) {
		Gen gen = new Gen();
		
		// 정수형
		Integer[] iArr = {1, 2, 3, 4, 5};

		// 더블형
		Double[] dArr = {1.1, 2.2, 3.3, 4.4, 5.5};

		// Character
		Character[] cArr = {'A', 'B', 'C', 'D', 'E'};

		//제네릭 이용
		//위의 배열들을 int, double, char와 같은 기본자료형으로 만들었다면
		//아래의 메서드에 대입할수 없다.
		//제네릭 타입은 반드시 객체를 처리하록 되어있다.
		gen.printArr(iArr);
		gen.printArr(dArr);
		gen.printArr(cArr);
	}
}
``` 
  
  
  
