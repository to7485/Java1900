### 열거형
열거형은 상수를 가지고 생성되는 객체들을 한곳에 모아둔 하나의 묶음이다.
상수를 사용자가 지정한 이름으로부터 0부터 순차적으로 증가시켜준다.

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
	}
}

```
