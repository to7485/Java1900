# 람다식
- 메서드를 하나의 ‘식(expression)’으로 표현한 것
- 제네릭타입은 자바1.5버전에서 도입됨
- 람다식은 자바1.8 버전에서 도입됨

## 람다식이 도입된 이유
- 함수형 프로그래밍 방식
- 자바에서는 함수형 프로그래밍 방식이 적용되지 않았다.
- 자바 공부할 때 함수는 어디에 만들었는가 클래스를 나누어서 작성했었다.
- 자바 -> 함수가 독립적이지 않다. -> 반드시 객체를 만들어서 호출

타 프로그래밍 언어에서는 함수만 독립정으로 정의하는게 가능하다.(독립 프로그램이 된다)

- 자바스크립트의 예시 인터넷창 개발자도구 -> console탭에서 작성하기
```java
funtion add(num1,num2){
	return num1+num2;
}

add(10,20)
30
```
자바에서도 이렇게 독립적으로 함수를 사용하는 방법이 없겠느냐 해서 개발된 것

## 함수형 프로그래밍의 특징
1. 함수를 매개변수로 사용

예시 인터넷창 개발자도구 -> console탭에서 작성하기
```java
var fruits = [“apple”,”orange”,”melon”,”mango”]

fruits.forEach(function(fruits){
	console.log(fruit);
});
```

2. 함수를 반환값으로 사용

반환값 이라고 하는건 return인데 우리가 자바에서 함수를 공부하면서 return값에 함수를 넣어본적은 없다.
```java
funciton outerFunc(x){
	return function innerFunc(y) {
		return x + y;
	}
}

var innerFunc = outerFunc(10);
innerFunc(20);

30
```
함수를 단축하여 표현하는것도 가능하다.
```
fruits.forEach(fruit => console.log(fruit));
```

요즘 개발 트렌드가 함수형 프로그래밍으로 바뀌고 있다<br>
자바도 어쩔수 없이 흐름을 따라갈수 밖에 없지만 완벽한 함수형 프로그래밍은 아니다.<br>
독립적으로 쓰이지 못하고 객체를 이용하여 호출해야 하는건 변함이 없다.<br>

자바에서 함수형 프로그램을 어떻게 구현하는지 문법에 대해서 먼저 알아보자.<br>



## 람다식 사용하기
1. 인터페이스
2. 구현할 메서드 선언
3. 메서드는 한 개만 정의 => 함수형 프로그래밍에서는 함수가 독립적으로 사용되기 때문, 함수 하나에 기능 하나 자바에서는 클래스 내부에 정의하게 되면 메서드가 한 개 이상 정의될 수 있다. 그래서 제한을 두고 있다.

프로젝트 생성하기<br>

calculator 패키지 생성하기<br>

#### MyCalculator 인터페이스 생성하기
```java
package calculator;

public interface MyCalculator {
	int plus(int num1,int num2);
}
```
#### Calculator 클래스 생성하기
```java
자바에서는 객체를 만들지 않으면 함수를 사용할 수 없다. 그래서 MyCalculator 객체를 만들어야 한다.
package calculator;

public class CalculatorImpl {
	public static void main(String[] args) {
		MyCalculator calc = (int num1, int num2)->{
			return num1 + num2;
		};
		
		int result = calc.plus(20, 30);
		System.out.println(result);
	}
}
```
인터페이스를 왜 구현하는 클래스를 만들지 않고 사용할 수 있는가??


#### Calculator2 클래스 만들기
```java
package calculator;

public class Calculator2 {
	public static void main(String[] args) {
		MyCalculator cal = new MyCalculator() {
			
			@Override
			public int plus(int num1, int num2) {
				// TODO Auto-generated method stub
				return 0;
			}
		};
	}
}
```
#### 인터페이스에 함수를 하나만 정의해야 하는 이유
- 클래스에서 람다식으로 사용할 때 이름을 사용하지 않기 때문에 어떤 함수인지 모른다.

어노테이션<br>
@FunctionalInterface<br>
내가 컴파일러에게 이 인터페이스를 람다식용 인터페이스로 쓸거다 라고 알려주는 것.<br>
그렇게 되면 인터페이스에 함수를 두개 쓰게 되면 오류가 난다.<br>
 
실수를 줄일 수 있다.<br>
```java
package calculator;

public class Calculator2 {
	public static void main(String[] args) {
		int num3 = 30;
		MyCalculator cal = new MyCalculator() {
			
			@Override
			public int plus(int num1, int num2) {
				//num3 = 40; -> final int num3 -> 지역변수의 상수화
				// TODO Auto-generated method stub
				return 0;
			}
		};
	}
}
```
#### Calculrator3 클래스만들기
```java
package calculator;

public class Calculator3 {
	public static void main(String[] args) {
		MyCalculator calc = (num1, num2) ->{
			return num1 + num2;
		};

		//중괄호와 return도 생략가능하다.
		MyCalculator calc2 = (num1, num2) -> num1 + num2;
	}
}
```
자료형도 생략이 가능하다 인터페이스에 정의가 되어있기 때문에!
 
자료형을 하나만 남겨놔도 안된다. 지우려면 다 지우자.

#### MyFunction 람다식 인터페이스 생성하기
```java
package calculator;

@FunctionalInterface
public interface MyFunction {
	void method(int num);
}
```
#### Calculator3 에 코드 추가하기
```java
package calculator;

public class Calculator3 {
	public static void main(String[] args) {
		MyCalculator calc = (num1, num2) ->{
			return num1 + num2;
		};
		
		//중괄호와 return도 생략가능하다.
		MyCalculator calc2 = (num1, num2) -> num1 + num2;
		
		//매개변수가 하나일 때는 소괄호가 생략이 가능하다.
		MyFunction myfunction = num -> System.out.println(num);
	}		
}
```

4.람다식을 이용하면서 가능한 부분은 최대한 생략하기
- 람다식을 매개변수로 사용하기

#### Calculrator4 클래스 만들기
```java
package calculator;

public class Calculrator4 {
	public static void main(String[] args) {
		MyCalculator calc = (num1,num2) -> num1 + num2;
		int result = myCalc(calc);
		System.out.println(result);
		
		int result2 = myCalc((num1,num2) -> num1 + num2);
		위 방법보다 간단하게 표현할 수 있다.

		System.out.println(result2);
	}
	
	static int myCalc(MyCalculator calc) {
		return calc.plus(1,2);
	}
}
```
#### Calculrator5 클래스 만들기
package calculator;

import java.util.*; java.util패키지에 있는 모든 것 import 하겠다.

public class Calculrator5 {
	public static void main(String[] args) {
		ArrayList<String> list = new ArrayList<String>();
		list.add("이름1");
		list.add("이름2");
		list.add("이름3");
		list.add("이름4");
		list.add("이름5");
		
		list.forEach();
	}
}
```
ArrayList에 forEach()메서드가 있고 Consumer 라는 매개변수를 받는다 자바 공식문서에서 검색해보면 FunctionalInterface라는걸 알 수 있다. 때문에 람다식으로 표현할 수 있다.

 
https://docs.oracle.com/javase/8/docs/api/java/util/function/Consumer.html

#### Calculrator5 클래스에 코드 추가하기
```java
package calculator;

import java.util.*;

public class Calculrator5 {
	public static void main(String[] args) {
		ArrayList<String> list = new ArrayList<String>();
		list.add("이름1");
		list.add("이름2");
		list.add("이름3");
		list.add("이름4");
		list.add("이름5");
		
		list.forEach(x -> System.out.println(x));
		list.forEach(System.out::println);
	}
}
```

