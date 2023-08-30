# while문
- 간편한 구성을 가진 반복문(선비교 후처리)
- 반복 횟수가 정해져 있지 않고 조건식이 true일 경우 계속해서 반복하는 문법.
- for문보다 구조가 간단하기는 하지만 주의해서 사용하지 않으면 무한 루프 같은 오류에 빠지기 쉽다.

```java
while(조건식){
    조건식이 참일때 반복할 명령
}
```
- while문은 for문처럼 시작값과 증감값을 가지고 있지 않기 때문에 값을 변화시켜주지 않으면 무한반복이 일어나게된다.

```java
int num = 1;
		
while(num <= 10){ 
	System.out.println(num);
}//while문의 끝
```

```java
int num = 1;
		
while(num <= 10){ 
	System.out.println(num);
	num++;
}//while문의 끝
```
## do-while문
- while문은 선비교 후처리를 하지만
- do-while문은 선처리 후비교를 하기 때문에 조건에 맞지않아도 무조건 한번은 실행을 하게 된다.
- 제어문 중 유일하게 뒤에 세미콜론(;)을 붙혀야 한다.

```java	
int i = 11;
do{
    System.out.println(i);

}while(i <= 10); //결과 : 11
```
```java
int sum = 0;
int i = 1;

do {
	sum += i;
	i++;
} while(i <= 10);

System.out.println("합  : " + sum);
```

### 상황에 따라 반복문 사용하기
- 반복횟수가 지정되는 경우 -> 횟수를 만족할 때 까지 반복
    - ex) 물통에 물을 10번 채워라 -> for문
- 특정 조건이 부여되는 경우 -> 조건이 만족할 때까지 반복(물이 다 차기 전까지)
    - ex) 물통에 물이 가득 찰 때까지 채워라 -> while문
- 특정 조건과 옵션이 부여되는 경우 -> 한 번 실행한 후 반복 여부 판단
    - ex) 물통에 물을 따라보고 새지 않으면 끝까지 채워라 -> do - while문

# 기타제어문
- 일반적으로 조건식의 검사를 통해서 반복문에 진입하게 되면, 다음 조건식을 검사하기 전까지 반복문에 안에 있는 모든 명령을 실행한다.
- 기타제어문을 통해 반복문 자체의 흐름을 개발자가 직접 제어할 수 있다.
- 기타제어문에는 break와 continue가 있다.
## break
- 반복문 내에서 break를 만나게 되면 가장 가까운 반복문을 종료하고 다음 코드를 실행하게 된다.
```java
for(int i = 1; i <= 2; i++){ 
	             for(int j = 1; j <= 5; j++){ 
	
         if(j % 2 == 0){//j 를 2으로 나눈 나머지가 0일때
          break;// 가장 가까운 반복문 탈출!
         }
	          System.out.print(" " + j);
    }//안쪽 for문의 끝
	System.out.println();//줄 바꿈!
}//바깥쪽 for문의 끝
```
- while문과 break
```java
int n = 1;
	
while (true) {//무한반복. !true나 false는 불허
	System.out.println(n);
n++;
	
//n이 10보다 클 때 break로 while문을 빠져나오는 구문을 만들어보자	

if(n > 5){
	break;
  }
}
```
## continue
- 반복문 내에서 continue를 만나게 되면 가장 가까운 반복문의 증감식으로 돌아간다.(증감식이 없을 때 조건식으로 돌아간다)

```java
public class Ex1_continue {
	public static void main(String[] args) {
		
		//continue문 : 반복문 내에서 특정 문장을 건너뛰고자 할 때 사용
		
		for( int i = 1; i <= 2; i++) {
			
			for(int j = 1; j <=5;) {
				
				if(j % 2 == 0) {
				//가장 가까운 반복문의 증감식으로 이동, 증감식이 없다면 조건식으로 이동
					continue;
				}
				j++;
				
				System.out.print(j + " ");
			}//inner
			System.out.println();
		}//outer
		
	}//main
}
```
- continue와 while문
```java
public class Ex2_continue {
	public static void main(String[] args) {
		
		int n = 0;
		
		while(n < 10) {
			n++;
			
			if( n % 2 != 0) {
				//while문에서 continue를 만나면 조건식으로 이동
				continue;
			}
			
			System.out.println(n);
		}//while
		
```
## label
- 일반적인 기타제어문은 단 하나의 반복문만을 이동하게 해줍니다.
- break,continue에 라벨을 달아서 가장 가까이 있는 반복문이 아닌 내가 원하는 반복문을 빠져나오거나,이동할 수 있게 한다.

```java
Ex3_label_break 클래스 생성
	//label: 특정 반복문에 이름표를 붙여 두 개 이상의 반복문을
	//       제어할 수 있도록 하는 키워드
	
	//label은 항상 쌍으로 존재한다.
	//label의 이름은 자기가 원하는대로 사용이 가능하다.
	
	//label은 자신을 포함하고 있는 상위 개념에게만 달 수 있다.
	
	happy: for (int i = 1; i <= 3; i++) {
	
		for (int k = 1; k <= 10; k++) {
			System.out.println(k + " ");
		}
	
		for (int j = 1; j <= 10; j++) {
	
			if (j % 2 == 0) {
				break happy;
			}
			System.out.print(j + " ");
		} // inner
		System.out.println();
	} // outer
}

--------------------------------------------------------------------예제1
continue 패키지에 클래스 만들기
Ex3_label_continue 클래스 생성
int n = 0;
		
outer : while(true){
	
if( n >= 10) //이 부분은 무한반복 되는거 확인후 가장 마지막에 추가.	
		break;
	while(true){
	
n++;		
if(n % 3 == 0){
	System.out.println("continue를 만남");
	continue outer;	System.out.println(n);
	
}
--------------------------------------------------------------------------------
switch속의 break
n = 0;
		
w : while( n < 10) {
	
	n++;
	
	switch( n ) {
	case 1:
		System.out.println("switch문 1번 거쳐감");
		//switch문에서 break는 반복문을 나가는게 아닌 switch문만 나가게 된다.
		break w;
		
	case 2:
		System.out.println("switch문 2번 거쳐감");
		//switch문만 단독으로 사용을 할 때는 continue를 사용할 수 없다.
		continue;
	
	}//switch
	System.out.println(n);
	
}//while

```

# 배열(Array)
- 같은 자료형의 변수를 지정하여 여러 데이터를 저장할 수 있는 저장공간을 의미한다.
- 이렇게 여러 데이터를 담을 수 있는 구조를 자료구조(data structure)라고 한다.
- 배열을 사용하면 같은 자료형의 데이터를 효율적으로 다룰 수 있다.

## 배열의 선언
![image](https://user-images.githubusercontent.com/54658614/215389995-4398cf1e-78c8-4969-8478-1a3fb9a741a1.png)

- 대괄호[]는 배열의 연산자를 의미한다.
- 자료형 뒤에 붙이거나 변수명 뒤에 붙이면 해당 자료형은 배열이라는 의미로 선언된다.
- 자료형 뒤에 붙이는것이 가독성이 좋아 자주 사용된다.

## null
```java
int num;
```
- 해당 변수는 어떤 값을 가질지 알 수 없다.
- 만약 변수를 만들 때 값을 부여하지 않으면 시스템이 타입에 맞는 불특정 값을 부여하게 된다.
- 따라서 변수를 만들 때, 어떤 값이 부여되는지 쉽게 알기 위해 다음과 같이 초기값을 부여하면서 선언하도록 했다
```java
int num = 0;
```

- 배열의 경우는 여러 개의 데이터를 저장하기 위한 별도의 공간이 필요하다.
- 배열을 선언만 하고 생성하지 않을 경우, 시스템은 배열을 만들 때 null 이라는 키워드를 부여한다.
- null의 의미는 "없다"라는 의미를 가진다.
- 배열 변수는 만들어졌지만 그 안에 값을 담을 공간들이 생성되지 않았다는 뜻이다.
- 신차를 만들 때 이름은 정해서 발표했지만, 실제로 자동차는 아직 생산되지 않은 상태이다.

## 배열의 생성
![image](https://user-images.githubusercontent.com/54658614/215390064-8eaa5306-29c6-4aa4-9acb-86f377d1f8d2.png)

## 선언과 생성을 동시에 하는것도 가능하다.
![image](https://user-images.githubusercontent.com/54658614/215390219-ebbe71be-fd12-46b5-8d31-a12f98307c21.png)

- 배열에 저장될 값을 미리 부여해 선언하는 방법이 있다.
```java
int[] arr = {1,2,3,4,5}
```
- 위와 같이 배열을 선언할 때 값을 지정할 수 있다.
- 5개의 값을 대입했기 때문에, 배열의 크기는 5가 되며 각 순서에 맞게 데이터가 삽입된다.
- 해당 방법은 배열을 최초 선언할 때만 가능하다.

```java
int[] arr; //배열선언
arr = {1,2,3,4,5} //오류
```
- 배열을 선언한 후 다시 값을 대입해야할 경우에는 이미 선언된 배열을 다시 정의하여 값을 대입하면 가능하다.
```java
int [] arr;
arr = new int[]{1,2,3,4,5};
```
- 위와 같은 방법들을 통해서 배열을 선언하면 실제 시스템 메모리에는 선언된 크기와 값 만큼 각각의 독립적인 저장 공간이 연속적으로 배치되어 생성된다.

![image](https://user-images.githubusercontent.com/54658614/215388446-0a8c33c5-5e62-4798-b98b-d445511574a6.png)

- 메모리에 지정한 크기만큼의 저장 공간을 생성하고 그 저장 공간이 있는 위치 값을 arr 변수에 대입한다.
- 배열의 변수는 그 주소 값을 통해서 배열에 접근하는 데이터를 가져오게 된다.

## Ex1_Array 클래스
```java
package test;

public class Test{
	public static void main(String[] args) {
		
		int[] arr = new int[4];
		
		System.out.println(arr);
				
	}
}

[I@7d6f77cc
```
- [X@xxx...과 같은형태로 출력이 될것이다.
- 이 값은 배열이 위치한 주소값이다.
- 이처럼 값을 직접 변수에 저장하는것이 아니라 주소값이 저장되어 해당 주소를 통해 실제 주소에 접근한다.
- 이를 참조변수라고 한다.

## 배열의 특징
- 배열 선언 시 크기를 지정한다.
- 배열 선언 후 공간의 크기를 늘리거나 삭제할 수 없다.
- 지정된 자료형의 값만 저장할 수 있다.

## 배열의 구조
1. 인덱스(index)
    - 배열을 만든 후에는 값을 넣거나 꺼내야 한다.
    - 배열은 각 공간마다 위치를 알려주는 위치 값이 존재한다.
    - 우리는 배열이 지니는 값들의 위치를 인덱스(index)라고 부른다.
    - 인덱스(index)는 배열의 공간마다 붙여진 번호로 0부터 시작하여 순차적으로 증가한다.

```java
// 1) 배열선언
int[] ar;

// 2) 배열생성
//배열의 index수의 갯수는 처음 지정해둔 갯수에서 강제로 늘리거나 줄일 수 없다.
//스택과 힙에 대한 설명  기본자료형 변수와 데이터는 스택에 만들어진다.
//클래스 구조와 배열구조는 스택에 일단 만들어진다. new 라는 키워드를 통해서 힙 메모리 영역에 집을 지어주는 키워드이다.
ar = new int[4];

//생성 후에는 값을 넣어 초기화가 필요하다.
//아무런 값도 넣지않으면 기본자료형은 각 자료형의 초기값,
//스트링형은 null이 들어간다.
//int[] ar = {100, 200, 300, 400};//초기화 방법1

// 3) 초기화 방법2
ar[0] = 100;
ar[1] = 200;
ar[2] = 300;
ar[3] = 400;
//배열의 출력		
System.out.println(arr[0]);
System.out.println(arr[1]);
System.out.println(arr[2]);
System.out.println(arr[3]);
```
2. 배열의 길이
    - 배열을 생성할 때 대괄호[]안에 배열의 길이를 작성했다.
    - 배열을 사용하면서 종종 배열의 길이가 필요할 때가 있다.
    - 배열은 내부적으로 length라는 변수를 지니는데, 해당 변수는 배열의 길이 값을 가지고 있다.
    - 배열의 길이를 알고싶을 때는 '배열명.length'를 하면 된다.
    - 이 변수의 값은 배열이 생성될 때 지정되며 변경할 수 없다.

```java
//배열의 출력2
//ar.length : 배열의 방의 개수
for(int I = 0; I < ar.length; I++){
	System.out.println(ar[i]);
}
```
3. 배열의 초기값
    - 배열은 생성과 동시에 데이터 자료형 별로 기본값이 주어진다.
    - 배열을 선언했을 때 저장되는 초기값을 자료형 별로 정리하면 다음과 같다.
|자료형|초기값|
|------|------|
|정수형|0|
|실수형|0.0|
|문자형|''|
|객체형|null|

```java
package test;

public class Test{
	public static void main(String[] args) {
		
		//5개의 공간을 가지는 배열선언
		int [] intArray = new int[5];
		String[] strArray = new String[5];
		
		//5개의 값을 가지는 배열 선언
		int [] varArray = {1,2,3,4,5};
		
		//intArray의 첫번째 값 출력
		System.out.println("intArray[0] : "+intArray[0]);
		//intArray의 두번째 값 출력		
		System.out.println("intArray[1] : "+intArray[1]);
		//strArray의 첫번째 값 출력
		System.out.println("strArray[0] : "+strArray[0]);
		//strArray의 두번째 값 출력		
		System.out.println("strArray[1] : "+strArray[1]);
		//varArray의 첫번째 값 출력
		System.out.println("varArray[0] : "+varArray[0]);
		//varArray의 두번째 값 출력		
		System.out.println("varArray[1] : "+varArray[1]);		
	}
}
```

## 배열 사용하기
- Ex3_Array 클래스 생성하기
```java
public class ArrayEx3 {
	public static void main(String[] args) {
		char[] ch;
		ch = new char[4];
		//char[] ch = new char[4];
		
		//배열 초기화
		ch[0] = 'J';
		ch[1] = 'A';
		ch[2] = 'V';
		ch[3] = 'A';
		
		//배열 내용 출력
		for(int i = 0; i < ch.length; i++){
			System.out.printf("ch[%d] : %c",i,ch[i]);
		}


		String[] str = new String[3];
		str[0] = "hello";
		
		for(int i = 0; i < ch.length; i++) {
			System.out.print(ch[i]);
		}
		System.out.println();
    
    		System.out.println(ch); //문자형 배열은 배열의 이름만으로도 전체 내용을 출력할 수 있다.
		
		System.out.println("----------------------------");
		
		System.out.println(str); //문자열 배열은 이상하게 나온다.

		//개선된 루프.
		//편리하지만, 배열의 각 요소에 대한 값의 수정과 삭제가 불가
		//for(char ch2 : ch)
			//System.out.println(ch2);
	}
}
```
```java
public class Ex2_array {
	public static void main(String[] args) {
		
		int [] iArr = new int[4];
		
		for(int i = 0; i < iArr.length; i++) {
			//초기화를 할 때 값을 반복문을 통하여 한번에 할당을 할 수 도 있다.
			iArr[i] = (i + 1)*100;
			System.out.println(iArr[i]);
		}
		
	}//main
}
```
## 실습문제
- 문제1
```java
//배열 arr에 담겨있는 모든 값의 합을 출력하시오
//결과 : 150

int[] arr = {10,20,30,40,50};

int total = 0;
for(int I = 0; I <arr.length; I++){
	total += arr[i];
}
System.out.printf("배열의 총 합 : %d\n",total);
```
-문제2
```java
프로그램이 실행되면 배열의 길이를 몇으로 할 것인지 물어본다.
예를들어 키보드에서 5를 입력받으면...

결과 : 
배열의 길이는 몇으로? : 5
ABCDE

public class Work_Ex1 {
	public static void main(String[] args) {
		
		System.out.print("배열의 길이는 몇으로? : ");
		Scanner scan = new Scanner(System.in);
		int n = scan.nextInt();
		
		char c[] = new char[n];
		char c2 = 'A';
		
		for(int i = 0; i < c.length; i++){
			System.out.print(c[i] = c2++);
		}
		
		// char ch[] = new char[n];
		// for(int i = 0; i < ch.length; i++){

		 // ch[i] = (char)('A' + i);
		 // System.out.print(ch[i]);
		// }		
	}
}
```
- 문제3
```java
변수 money에 10 ~ 5000사이의 난수를 발생시켜 넣는다.
단 3450,2100,60과 같이 1의자리 숫자는 반드시 0이 되도록 한다.

발생된 난수 money를 동전으로 바꾸면 각 동전이 몇 개씩 필요한지를 판단하는 코드 작성,

가능한한 적은 수의 동전을 사용하도록 한다.

//4170
//500원 : 8
//100원 : 1
//50원 : 1
//10원 : 2

int[] coin = {500,100,50,10};
int money = new Random().nextInt( 500 )+1
money *= 10;
System.out.println(“금액: ” + money);

for(int I = 0; I < coin.length; I++) {
     int res = money / coin[i];
     System.out.println( coin[i] + “원 : ” + res);
     money %= coin[i];
}//for
```
- 문제4
```java
1 ~ 45의 난수를 발생시켜 로또번호를 생성하는 프로그램 만들기.
public class MyLotto {
	public static void main(String[] args) {
		
		//로또번호 6개를 담을 배열 준비
		int[] lotto = new int[6];
		outer : for(int i = 0; i < lotto.length;){//나중을 위해 i++을 생략
			lotto[i] = new Random().nextInt(45) + 1;
			//중복값을 비교하는 반복문
			for(int j = 0; j < i; j++){
				if(lotto[i] == lotto[j]){
					continue outer;
				}					
			}//inner For
			System.out.print(lotto[i] + " ");
			i++;						
		}//outer For
	}
}
```












