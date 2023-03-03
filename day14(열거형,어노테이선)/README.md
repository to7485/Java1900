### 열거형
열거형은 상수를 가지고 생성되는 객체들을 한곳에 모아둔 하나의 묶음이다.
상수를 사용자가 지정한 이름으로부터 0부터 순차적으로 증가시켜준다.

- 상수만 들어갈 수 있다.

ex1_Enum 패키지 생성

#### Item enum 생성
![image](https://user-images.githubusercontent.com/54658614/221763228-0f755180-bb54-4e30-853a-acb27ede920e.png)
![image](https://user-images.githubusercontent.com/54658614/221763289-9b65b891-2087-4bb3-a2cc-c9a13d6144a2.png)

```java
package test;

public enum Item {START,STOP,EXIT}
```
### Enum클래스가 컴파일 될 때 자동 추가되는 메서드
- getDeclaringClass()
- name() : 열거형 상수의 이름을 문자열로 반환
- ordinal() : 열거형 상수가 정의된 순서를 반환
- valueof("상수명")
- valueof(Item.class, "START);
- values() : 열거형 상수안에 들어있는 내용들을 배열로 반환

### 열거형 데이터 비교 특징
- 열거형 상수간의 비교에는 ==을 사용할 수 있다.(상수의 주소를 비교)
- '<','>'와 같은 비교연산자는 사용할 수 없고 compareTo()는 사용이 가능하다.

#### Ex1_Enum 클래스 생성
```java
public class Ex1_Enum {

	public static void main(String[] args) {
		Item[] items = Item.values();
		System.out.println(Arrays.toString(items)); //Arrays 클래스 import
    
    //열거형 순서 반환해보기
		for(Item item : items) {
			System.out.println("name="+item.name()+",ordinal = "+item.ordinal());
		}
    
    Item i1 = Item.START;
		Item i2 = Item.valueOf("START");
		Item i3 = Item.valueOf(Item.class,"START");
		Item i4 = Item.STOP;
		System.out.println(i1 == i2);
		
		
    
    System.out.println(d1 > d4);//오류남
    
	switch(i1) {
	case START://Item.START라고 쓸 수 없다.
		System.out.println("게임시작!");
	break;
	case STOP:
		System.out.println("게임멈춤!");
	break;
	case EXIT:
		System.out.println("게임종료!");
	break;
	}

    }
}

```
열거형 클래스 안에 있는 상수에 직접 값을 입력할 수 있다.

#### Item enum클래스에 코드 추가하기
```java
public enum Item {
	START("시작",">"),STOP("멈춤","<"),EXIT("종료","V");//값을 직접 대입하면 생성자를 만들어줘야 한다.
	
	protected String itemStr;
	protected String Sysmbol
	하지만 다른 클래스에서 생성자를 호출할 수 없다.
	Item(String str){//private
	    this.itemStr = str;
	}
	
	public String getItemStr(){
		return itemStr;
	}
}


```

#### Ex2_Enum 클래스 생성하기
```java
package test;

public class Ex2_Enum {
	public static void main(String[] args) {
		
		/*
		 * Item start = Item.START; 
		 * String str = start.getItemStr(); //하나만 출력하기
		 * System.out.println(str);
		 */
		
		//향상된 for문을 이용하여 열거형의 전체내용 출력하기
		Item[] items = Item.values();
		for(Item item : items) {
			System.out.println(item.getItemStr());
		}
	}
}

```

#### Item enum클래스에 코드 추가하기
```java
package test;

public enum Item {
	START("시작",">"),STOP("멈춤","<"),EXIT("종료","V");//값을 직접 대입하면 생성자를 만들어줘야 한다.
	
	protected String itemStr;
	protected String symbol;
	
	Item(String str,String sysmbol){//private
	    this.itemStr = str;
	    this.symbol = symbol;
	}
	
	public String getItemStr(){
		return itemStr;
	}
	
	public String getSymbol(){
		return symbol;
	}
}

```
#### Ex2_Enum 클래스 코드 수정하기
```java
package test;

public class Ex2_Enum {
	public static void main(String[] args) {
		
		/*
		 * Item start = Item.START; 
		 * String str = start.getItemStr();
		 * System.out.println(str);
		 */
		
		Item[] items = Item.values();
		for(Item item : items) {
			System.out.printf("메뉴 : %s, 기호 : %s\n",item.getItemStr(),item.getSymbol());
		}
	}
}
```
열거형을 따로 따로 쓴다면
```java
public enum Item {
	START("시작","s"),STOP("멈춤","p"),EXIT("종료","e");
	
public class Item {
	public static final Item START =  new ITEM("시작","s");
	public static final Item STOP =  new ITEM("멈춤","p");
	public static final Item EXIT =  new ITEM("종료","e");
```

### 열거형에 추상메서드 추가하기
- 열거형에 추상 메서들르 선언하면 각 열거형 상수가 이 추상 메서드를 반드시 구현해야 한다.
- 추상클래스나 인터페이스를 가지고 추상 메서드를 구현함으로써 익명 클래스를 작성하는 것과 유사하다.

#### Transportaion 열거형 생성하기
```java
package test;

public enum Transportaion {
	BUS(100),
	TRAIN(150),
	SHIP(200),
	AIRPLANE(250);
	
	protected final int fare;
	
	Transportaion(int fare){
		this.fare = fare;
	}
	abstract int totalFare(int distance); //추상메서드를 적으면 구현을 해야 한다며 오류가 난다.
}

```
![image](https://user-images.githubusercontent.com/54658614/222339460-a50b9493-3eb5-4282-abd7-8b9588a81b96.png)

구현을 해주자

#### Transportaion 열거형 코드 추가하기
```java
package test;

public enum Transportaion {
	BUS(100){
		int totalFare(int distance){
			return distance*fare;
	}	
   },
	TRAIN(150){
	   int totalFare(int distance){
			return distance*fare;
	}	
   },
	SHIP(200){
	   int totalFare(int distance){
			return distance*fare;
	}	
   },
	AIRPLANE(250){
	   int totalFare(int distance){
			return distance*fare;
	}	
   };
	
	protected final int fare;
	
	Transportaion(int fare){
		this.fare = fare;
	}
	
	abstract int totalFare(int distance);//사실 추상클래스로 정의할 필요는 없긴하지만 추상클래스가 있을 때 어떻게 작성해야 하는지 보여주기 위한 예제
	//추상클래스가 들어갈 수 있다는 것은 enum도 추상클래스이다.
}

```
#### Ex3_Transportaion클래스 생성
```java
package test;

public class Ex3_Transportaion {
	public static void main(String[] args) {
		Transportaion[] trans = Transportaion.values();
		
		for(Transportaion tran : trans) {
			System.out.printf("name : %s, 100km - fare : %d\n",tran.name(),tran.totalFare(100));
		}
	}
}
```

열거형은 상수가 정적객체로 만들어진다고 보면된다.













