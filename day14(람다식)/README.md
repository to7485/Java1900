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
function add(num1,num2){
	return num1+num2;
}

add(10,20)
30
```
![image](https://user-images.githubusercontent.com/54658614/224224980-44b27fa7-25b3-4d2d-95ec-ad3a425798c7.png)


자바에서도 이렇게 독립적으로 함수를 사용하는 방법이 없겠느냐 해서 개발된 것

## 함수형 프로그래밍의 특징
1. 함수를 매개변수로 사용

인터넷 브라우저 -> f12눌러 개발자도구 열기 -> console탭으로 이동
```java
var fruits = ["apple","orange","melon","mango"]

fruits.forEach(function(fruit){
	console.log(fruit);
});
```
![image](https://user-images.githubusercontent.com/54658614/224224761-5a22b9ff-29c7-4e9a-90db-174535e80a53.png)


2. 함수를 반환값으로 사용

반환값 이라고 하는건 return인데 우리가 자바에서 함수를 공부하면서 return값에 함수를 넣어본적은 없다.
```java
function outerFunc(x){
	return function innerFunc(y) {
		return x + y;
	}
}

var innerFunc = outerFunc(10);
innerFunc(20);

30
```
![image](https://user-images.githubusercontent.com/54658614/224225240-1beb89d4-9e93-4f71-9660-53b8be840fad.png)


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
3. 메서드는 한 개만 정의 => 함수형 프로그래밍에서는 함수가 독립적으로 사용되기 때문, 
함수 하나에 기능 하나 자바에서는 클래스 내부에 정의하게 되면 메서드가 한 개 이상 정의될 수 있다. 그래서 제한을 두고 있다.<br>
	- 정적 메서드, default 메서드는 여러개 정의 가능

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
	
		//지역 내부 익명 클래스
		//익명 클래스는 내부 클래스(inner class)의 일종으로 이름이 없는 클래스를 말한다.
		//나중에 다시 불러질 이유가 없다는 뜻을 내포하고 있다.
		//즉, 프로그램에서 일시적으로 한번만 사용되고 버려지는 객체라고 보면 된다.(일회용 클래스)
		
		보통 어느 클래스의 자원을 상속 받아 재정의하여 사용하기 위해서는 먼저 자식이 될 클래스를 만들고
		상속(extends) 후에 객체 인스턴스 초기화를 통해 가능하다.
		하지만 익명 클래스는 클래스 정의와 동시에 객체를 생성할 수 있다.
		익명클래스는 이름이 없기 때문에 생성자를 가질 수 없으며, 가질 필요도 없다.
		
		MyCalculator cal = new MyCalculator() {
			
			@Override
			public int plus(int num1, int num2) {
				return num1 + num2;
			}
		};
	}
}
```

#### 인터페이스에 함수를 하나만 정의해야 하는 이유
- 클래스에서 람다식으로 사용할 때 이름을 사용하지 않기 때문에 어떤 함수인지 모른다.

![image](https://user-images.githubusercontent.com/54658614/224226019-2b79461e-208f-4815-8563-ace38207c754.png)

하지만 인터페이스에 여러개의 추상메서드를 정의해도 오류가 나지는 않는다.<br>
만약 람다식용으로 인터페이스를 사용할 것이라면 어노테이션을 지정해놔야 한다.<br>

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
			public int plus(int num1, int num2) {//내부 익명클래스로 만들었더라도 인터페이스 이기 때문에
				//num3 = 40; -> final int num3 -> 지역변수의 상수화
				// TODO Auto-generated method stub
				return 0;
			}
		};
	}
}
```

우리가 알던 방식과 다른 축약형으로 함수를 만들어보자<br>

4.람다식을 이용하면서 가능한 부분은 최대한 생략하기

#### Calculrator3 클래스만들기
```java
package calculator;

public class Calculator3 {
	public static void main(String[] args) {
		MyCalculator calc = (int num1,int num2) ->{
			return num1 + num2;
		};
		
		//자료형도 생략이 가능하다 인터페이스에 정의가 되어있기 때문에!
		//자료형을 하나만 남겨놔도 안된다. 지우려면 다 지우자.
		//중괄호와 return도 생략가능하다.
		MyCalculator calc2 = (num1, num2) -> num1 + num2;
	}
}
```


#### MyFunction 람다식 인터페이스 생성하기
```java
package calculator;

@FunctionalInterface
public interface MyFunction {
	//파라미터가 한개인 경우 생략해보기
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
		
		//::(이중콜론) : 메서드 참조 연산자.
		//람다식을 보다 간결하게 사용할 수 있도록 해준다.
		MyFunction myfunc = System.out::println;
	}		
}
```
### 람다식을 매개변수로 사용하기

#### Calculrator4 클래스 만들기
```java
package calculator;

public class Calculrator4 {
	public static void main(String[] args) {
		MyCalculator calc = (num1,num2) -> num1 + num2;
		int result = myCalc(calc);
		System.out.println(result);
		
		//위 방법보다 간단하게 표현할 수 있다.
		int result2 = myCalc((num1,num2) -> num1 + num2);
		System.out.println(result2);
	}
	
	static int myCalc(MyCalculator calc) {
		return calc.plus(1,2);
	}
}
```
#### Calculrator5 클래스 만들기

#### 컬렉션 프레임워크와 함수형 인터페이스
컬렉션 프레임워크의 인터페이스에 다수의 디폴트 메서드가 추가 되었고 그 중 일부는 함수형 인터페이스를 사용한다.<br>
ArrayList에 forEach()메서드가 있고 Consumer 라는 매개변수를 받는다 자바 공식문서에서 검색해보면 FunctionalInterface라는걸 알 수 있다.<br>
때문에 람다식으로 표현할 수 있다.<br>

-forEach()메서드 사용

```
void forEach(Consumer<? super T> action)
	↓↓↓↓
@FunctionalInterface
public interface Consumer {
    void accept(T t);
}
```


https://docs.oracle.com/javase/8/docs/api/java/util/function/Consumer.html


#### Calculrator5 클래스 생성하기
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
### 람다식을 반환값으로 사용하기

#### Calculrator6 클래스 생성하기

```java
package test;

public class Calculator6 {
	public static void main(String[] args) {
		MyCalculator calc = myCalc();
		System.out.println(calc.plus(30, 50));
		
	}
	
	static MyCalculator myCalc() {
		//MyCalculator calc = (num1,num2) -> num1 + num2;
		//return calc;
		
		return (num1,num2) -> num1 + num2;
	}
}

```
## java.util.function패키지
- 대부분의 메서드는 타입이 비슷하다
- 매개변수가 없거나 한 개, 두 개, 반환값이 없거나 한 개이다.
- 제네릭 메서드로 정의하면 매개변수나 반환 타입이 달라도 문제가 되지 않는다. 
- java.util.function 패키지에 일반적으로 자주 쓰는 형식의 메서드를 함수형 인터페이스로 미리 정의해 놓았다.
- 매번 함수형 인터페이스를 정의하기 보다는 가능하면 이 패키지의 인터페이스를 활용하는 것이 좋다.

#### java.util.function  패키지의 주효 함수형 인터페이스

|함수형 인터페이스|메서드|설명|
|----|-----|-----|
|java.lang.Runnable|void() run()|매개변수도 없고 반환값도 없음|
|Supplier<T>|T get()|매개변수는 없고 반환값만 있음|
|Consumer<T>|void accept(T t)|Supplier와 반대로 매개변수만 있고, 반환값이 없음|
|Function<T,R>|R apply(T t)|일반적인 함수. 하나의 매개변수를 받아서 결과를 반환|
|Predicate<T>|boolean test(T t)|조건식을 표현하는데 사용됨.   매개변수는 하나. 반환값은 boolean|

###### 참고) 타입문자 'T'는 'Type'을 'R'은 'Return Type'을 의미한다.

#### 매개변수가 두 개인 함수형 인터페이스

매개변수가 두 개인 함수형 인터페이스는 이름 앞에 접두사 'Bi'가 붙는다.

|함수형 인터페이스|메서드|설명|
|----|-----|-----|
|BiConsumer<T,U>| void accept(T t, U u)|두개의 매개변수만 있고 반환값이 없음|
|BiPredicate<T,U>|boolean test(T t, U u)|조건식을 표현하는데 사용됨.   매개변수는 둘, 반환값은 boolean|
|BiFunction<T,U,R>|R apply(T t, U u)|두 개의 매개변수를 받아서 하나의 결과를 반환|

- 참고) Supplier는 매개변수는 없고 반환값만 존재하는데, 매서드는 두 개의 값을 반환할 수 없으므로 BiSupplier가 없다.
- 두 개 이상의 매개변수를 갖는 함수형 인터페이스가 필요하면 직접 만들어 써야 한다.

ex2_function 패키지 생성

#### Ex1_function 클래스 생성

![image](https://user-images.githubusercontent.com/54658614/224505449-4aeb4039-3830-4aea-a6be-3704f4759f39.png)

```java
package test;

import java.util.ArrayList;

public class Test {
	public static void main(String[] args) {

		ArrayList<Integer> list = new ArrayList<Integer>();
		for(int i = 1; i <=10; i++) {
			list.add(i);
		}
		list.removeIf(x -> x %2 == 0);//홀수만 반환
		System.out.println(list);
	}
}
```
#### 컬렉션 프레임워크와 함수형 인터페이스

컬렉션 프레임워크의 인터페이스에 다수의 디폴트 메서드가 추가 되었고 그 중 일부는 함수형 인터페이스를 사용한다.
	
|인터페이스|메서드|설명|
|----|-----|-----|
|Collection|boolean removeIf(Predicate<E> filter)|조건에 맞는 요소를 삭제|
|List|void replaceAll(UnaryOperator<E> operator)|모든 요소를 반환하여 대체|
|Iterable|void forEach(Consumer<T> action)|모든 요소를 변환하여 대체|
|Map|V compute(K key, BiFunction<K,V,V> f)|지정된 키의 값에 작업 f를 수행|
|Map|V computeIfAbsent(K key, Function(K,V) f)|키가 없으면 작업 f 수행 후 추가|
|Map|V computeIfPresent(K key, BiFunction(K,V,V) f)|지정된 키가 있을 때 작업 f수행|
|Map|V merge(K key, V value, BiFunction(V, V, V) f)|모든 요소에 병합작업 f를 수행|
|Map|void forEach(BiConsumer<K,V> action)|모든 요소에 작업 action을 수행|
|Map|void replaceAll(BiFunction(K,V,V) f)| 모든 요소에 치환작업 f를 수행|

#### Ex2_function 클래스 생성
```java
package test;

import java.util.ArrayList;
import java.util.HashMap;
import java.util.Map;

public class Test {
	public static void main(String[] args) {

		HashMap<String, String> map = new HashMap<String, String>();
		map.put("id1","이름1");
		map.put("id2","이름2");
		map.put("id3","이름3");
		map.put("id4","이름4");
		map.put("id5","이름5");
		
		//compute() : Map의 value값을 업데이트할 때 사용합니다.
		/*
		map.compute("id1", (k,v)->{
			return v+"**";
		});	
		
		System.out.println("map.get(\"id1\") : "+map.get("id1"));
		*/
		map.forEach((key,value)->{
			map.compute(key, (k,v)-> v+"**");
		});
		
		map.forEach((key,value)->{
			System.out.printf("key = %s, value = %s\n",key,value);
		});
		
		//Map.Entry :  Map 인터페이스의 내부 인터페이스이다.
		//Map에 저장되어 있는 key-value쌍을 다루기 위해 내부적으로 Entry 인터페이스를 정의해놓았다.
		//Map인터페이스를 구현하는 클래스 에서는 Map.Entry 인터페이스도 함께 구현해야 한다.
//		for(Map.Entry entry : map.entrySet()) {
//			System.out.printf("key = %s, value = %s\n",entry.getKey(),entry.getValue());
//		}
	}
}
```
#### UnaryOperator와 BinaryOperator
- Function의 변형이다
- 매개변수의 타입과 반환타입의 타입이 모두 일치한다.
- UnaryOperator와 BinaryOperator의 상위 인터페이스는 각각 Function, BiFunction이다.
	
|함수형 인터페이스|메서드|설명|
|----|-----|-----|
|UnaryOperator<T>|T apply(T t)|Function의 하위 인터페이스, Function과 달리 매개변수와 결과의 타입이 같다.|
|BinaryOperator<T>|T apply(T t, T t)|BiFunction의 하위 인터페이스, BiFunction과 달리 매개변수와 결과 타입이 같다.|

#### Ex3_function 클래스 생성
```java
package test;

import java.util.function.BinaryOperator;
import java.util.function.UnaryOperator;

public class Test {
	public static void main(String[] args) {

		int result = square(10,x -> x*x);
		
		int result2 = multi(10,20,(x,y) -> x*y);
		
	}
	
	public static int square(int num1,UnaryOperator<Integer> oper) {
		return oper.apply(num1);//언박싱 발생
	}
	
	public static int multi(int num1, int num2, BinaryOperator<Integer> oper) {
		return oper.apply(num1, num2);
	}
}
```
https://docs.oracle.com/en/java/javase/19/docs/api/java.base/java/util/function/package-summary.html
