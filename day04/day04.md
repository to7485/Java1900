## 반복문
### 특정 수행문을 여러번 반복할 수 있도록 해주는 제어문

반복문: 특정수행문을 원하는만큼 반복하여 실행하는 제어문<br>
for문 : 특정 명령을 원하는 만큼 반복적으로 처리할 때 사용한다.<br>

```java
		for(초기식; 조건식; 증감식){
				조건식에 해당할때 반복할 명령
		}
```
초기식 : 반복을 하기 위한 시작값으로 변수를 하나 초기화 한다.<br>
조건식 : 반복을 하기 위한 종료값으로 비교연산자를 많이 사용한다.<br>
증감식 : 변수의 값을 증감시켜주는 역할을 한다 증감연산자를 많이 사용한다.<br>
<br>
※후행증감이나 선행증감이나 영향은 없지만 개발자들이 다들 후행증감을 사용하므로 후행증감으로 사용하도록 하자.<br>
<br>


```java
for(int i = 0; i <= 3; i++){
	System.out.println(i);
}//for문 돌아가는 구조 설명해주기.
```

문제 : 1부터 10까지 반복하는 for문을 작성해보자.
for(int i = 1; i <= 10; i++){
	System.out.println(i);
}

문제 : 10부터 1까지 감소하는 for문을 작성해보자.
for(int i = 10; i >= 1; I--){
	System.out.println(i);
}

문제 - 1부터 10까지 반복하는 문장에서 3의 배수만 출력하는 제어력을 갖추어 보자!	
for(int i=1; i<=10 ; i++){
	if(i%3 == 0)
		System.out.println(i + “은(는) 3의 배수입니다.”);
}//for의 끝!

문제 - 1부터 20까지 홀수를 차례대로 출력해보자.
package sample public class Sample {
 public static void main(String[] args) {
  int i;
 for( i=1; i<=19; i++) {
        if(i%2!=0) {
             System.out.print(i+" ");
        } //if
     } //for
   }//main
 }
---------------------------------------------------------------------------
// 보너스 난수발생

// 예) 1부터10까지 수 중 난수를 발생시키기
// new Random().nextInt( (큰 수- 작은 수) + 1 ) + 작은 수
// new Random().nextInt( (10 - 1) + 1 ) + 1
int num = new Random().nextInt(10) + 1;
System.out.println(num);


예제2 - 난수를 사용한 구구단 출력
//2 ~ 9사이의 난수를 입력받아 구구단 출력하기
int random = new Random().nextInt(8) + 2;
		
for(int i = 1; i <= 9; i++){
	System.out.println(random + " * " + i + " = " + (random * i));
}
