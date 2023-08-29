# 반복문2

## while문
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

## 예제





