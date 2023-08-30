# 클래스

## 객체지향 프로그래밍
- 객체 지향 프로그래밍이란, 말 그대로 객체를 지향하는 프로그래밍 방법을 말한다.
- 객체란 우리 실생활에 존재하는 모든것으로 생각할 수 있다.
- 객체는 일반적으로 상태를 표현할 수 있고, 우리가 행동으로 실행할 수 있는 모든것들을 의미한다.
- 이런 객체를 중심으로 프로그램 구조를 설계하고 프로그래밍 하는 것을 객체 지향 프로그래밍이라고 한다.

## 클래스란?
- 객체를 생성하기 위한 설명서이다.
- 어떤 물건을 만들기 위한 메뉴얼이라고 생각하면 된다.
- 클래스를 기반으로 객체를 생성해야 한다.
- 하나의 설명서로 여러개의 물건을 만들 수 있듯이, 자바에서는 하나의 클래스로 여러 개의 객체를 새성할 수 있다.

## 클래스의 종류
- 실행용 클래스 
  - 프로그램 전체에서 단 하나의 클래스로, 프로그램의 실행을 맡고 있다.
  - main메서드를 갖고 있으며, 다른 클래스에서 사용하지 않는다.
- 객체 생성용 클래스
  - 다른 클래스에서 사용할 목적으로 선언되는 클래스 입니다.
- 하나의 클래스가 위 두 가지 용도의 역할을 모두 수행할 수 도 있다.
- 하지만 유지 보수와 객체 지향 프로그래밍의 특징인 모듈화를 고려해 별도로 분리하여 작성하는 것이 좋다.
- 일반적으로 하나의 프로그램에서 실행용 클래스 1개를 제외한 나머지 클래스는 모두 참조용 클래스이다.

## 클래스의 선언

## String 클래스
자바로 만들어진 모든 프로그램은 클래스로 이루어져 있습니다.
우리가 문자열을 저장하기 위해 사용했던 String도 자바에 내장되어있는 클래스입니다.

[자바문서](https://docs.oracle.com/javase/8/docs/api/index.html)

```java
package ex_String;

import java.util.Scanner;

public class Ex1_String {
		public static void main(String[] args) {
			
			//String클래스는 두가지 특징을 갖고 있다.
			//1)객체 생성법이 두가지(암시적, 명시적)
			//2)한 번 생성된 문자열의 내용은 변하지 않는다(불변의 특징)
			
			String s1 = "abc";//암시적 객체생성
			String s2 = "abc";
			//이미 앞에 같은 문자열로 생성된 암시적 객체가 있다면
			//앞서 생성된 객체의 주소를 재사용한다.

힙영역에 데이터가 생성되는건 모두 객체라고 한다.
			
			String s3 = new String("abc");//명시적 객체 생성
			String s4 = new String("abc");

자바의 모든 클래스들 중에서 new를 사용하지 않고 만들 수 있는건 String 밖에 없다. String도 클래스인데 마치 자료형처럼 사용할 수 있는 이유.
			
			
			// == 연산자는 기본자료형을 비교할 때는 값을 비교한다.
			//그러나 객체끼리 비교를 할 때는 주소를 비교하는 연산자로 기능이 바뀐다.
			if(s1 == s2) {
				System.out.println("주소가 같습니다.");
			} else {
				System.out.println("주소가 다릅니다.");
			}
			System.out.println("-------------------------------");
			if(s3 == s4) {
				System.out.println("주소가 같습니다.");
			} else {
				System.out.println("주소가 다릅니다.");
			}
			System.out.println("-------------------------------");
			
			if(s3.equals(s4)) {
				System.out.println("내용이 같습니다.");
			} else {
				System.out.println("내용이 다릅니다.");
			}
			System.out.println("------------------------------");
			
스캐너를 사용을 해봤는데 코드를 다시 한번 살펴 보자.

			Scanner sc =new Scanner(System.in);
			System.out.println("문자열: ");
			String s5 = sc.next();
			
			
			if(s5 == s1) {
				System.out.println("값이 같습니다.");
			} else {
				System.out.println("값이 다릅니다.");
			}
			
			System.out.println("--------------------------------");
			//불변의 특징
			
			
			String greet = "안녕";
			greet +="하세요";
			System.out.println(greet);
			
처음에 안녕 이라고 적인 메모리 영역이 힙에 할당 되는데 하세요가 붙는순간 안녕 뒤에 붙는게 아닌
안녕하세요 라고 하는 메모리를 새로 할당 받는다 그러면 남아있는 안녕이 메모리를 낭비시킬수 있는데
JVM의 GC가 힙 영역을 돌며 사용하지 않는 쓰레기 데이터를 주워간다.
			
			
			
		}//main
}
```
### String 클래스의 메서드들
메서드란! 어떤 작업을 수행하기 위한 명령문의 집합이다!!!<br>
메서드를 사용하는 작성하는 가장 큰 이유는 반복적으로 사용되는 코드를 줄이기 위해서이다.<br>
자주 사용되는 내용의 코드를 메서드로 작성해 두고 필요할때마다 호출만 하면 된다.<br>
```java
indexOf, lastIndexOf, charAt, substring, split정도만 설명. api보면서 하면 더 좋겠지만
융통성있게 하자


String str = "Kim Mal Ddong";
System.out.println("문자열 str의 길이 : " + str.length());
		
int index = str.indexOf('k');
System.out.println("맨 처음 문자 k의 위치 : " + index);//대소문자 구별 함
	
index = str.indexOf("Mal");
System.out.println("문자열 Mal의 위치 : " + index);//띄어쓰기 포함
	
index = str.lastIndexOf('n');
System.out.println("마지막 문자 n의 위치 : " + index);
		
char c = str.charAt(4);
System.out.println("추출한 문자 : " + c);
		
String str2 = str.substring(0, str.indexOf('M'));
System.out.println("0번째부터 M앞자리까지 글자 잘라내기 : " + str2);
System.out.println("잘라낸 str2의 길이 : " + str2.length());//길이는 띄어쓰기 포함 1부터 증가

스트링은 아니지만 스트링으로 작성된 숫자형태의 문자열을 실제 정수로 바꿔주는 코드
String number = "1";
System.out.println(Integer.parseInt(number) + 10);

int number = 1;
String s1 = Integer.toString(number);
System.out.println(s1);
		
String arr[] = str.split(" ");//띄어쓰기를 기준으로 분할

for(int i = 0; i < arr.length; i++)
	System.out.println("arr[" + i + "] : " + arr[i]);
```

### String 클래스의 메서드를 이용한 실습문제
```java
키보드에서 숫자와 특수문자를 제외한 알파벳을 무작위로 입력받는다.
입력받은 문자열에 소문자 a가 몇 개 있는지를 판별하는 로직을 구현해보자.

결과 : 
입력 : asdfasdf
a의 갯수 : 2

풀이 : 
public class Work_Ex1 {
	public static void main(String[] args) {

		String str;
		int count = 0;
		
		System.out.print("입력 : ");
		Scanner scan = new Scanner(System.in);
		str = scan.next();
		
		for(int i = 0; i < str.length(); i++){
			if(str.charAt(i) == 'a'){
				count++;
			}
		}
		
		System.out.println("a의 갯수 : " + count);
	}
}
-------------------------------------------------------------------------
자바 강의 1주차(3) 문제(String) - 3
회문수 구하기.
회문수란 앞으로 읽어도 뒤로 읽어도 똑같이 읽히는 숫자를 말합니다. 예를들어 12121과 같은 숫자.

키보드에서 세자리 이상의 숫자를 입력받은 후 해당 숫자가 회문수인지 아닌지를 판단하는 로직을 구현하자.

단, String클래스의 메서드를 활용하는 문제이니만큼, 키보드에서 입력받는 숫자는 String변수에 담아서 활용할수 있도록 한다.

풀이 :
public class Work_Ex3 {
	public static void main(String[] args) {
		
		String str = "";
		String str2 = "";
		
		System.out.print("3자리 이상의 숫자를 입력하세요 : ");
		Scanner scan = new Scanner(System.in);
		str = scan.next();
		
		for(int i = str.length(); i > 0; i--){
			str2 += str.charAt(i-1);
		}
		
		if(str.equals(str2)){
			System.out.println(str + "은 회문수 입니다.");
		}else{
			System.out.println(str + "은 회문수가 아닙니다.");
		}			
	}
}
-------------------------------------------------------------------------
자바 강의 1주차(3) 문제(String) - 4
아래와 같은 결과를 반영하는 로직을 구현해보자.

결과)

주민번호를 모두 입력하세요(-포함)
예)911223-203345
>> 991122-1122333
당신은 1999년 11월 22일에 태어난 남자입니다.


풀이)
public class Work {
	public static void main(String[] args) {
		
		System.out.println("주민번호를 모두 입력하세요(-포함)");
		System.out.println("예)911223-203345");
		System.out.print(">> ");
		Scanner scan = new Scanner(System.in);
		String id = scan.next();

		if(id.trim().length() < 14 || id.trim().charAt(6) != '-'){

			System.out.println("주민번호를 올바르게 입력하세요.");

		}else{

			String year = "";
			String result = "";

			year = id.substring(0, 2);

			if(Integer.parseInt(year) <= 14){
				result = "당신은 20";
			}else{
				result = "당신은 19";
			}
			result += year + "년 "
					+ id.substring(2, 4) +"월 " 
					+ id.substring(4, 6)
					+ "일에 태어난 ";

			if(id.charAt(7)%2 != 0){
				result += "남자입니다.";
			}else{
				result += "여자입니다.";
			}

			System.out.println(result);

		}//else

	}//main
}
```





