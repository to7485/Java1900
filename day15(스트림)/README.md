# Stream
기존의 Java에서 컬렉션 데이터를 처리할 때 특정 조건에 따라 필터링을 하려면 복잡한 과정을 거쳐야 했다.

반면에 SQL문법의 경우 사용자가 원하는 조건의 데이터를 목록을 검색할 때 명시적이고 간단한 방법을<br>
이용했는데 Java8 에서 새로 추가된 기능인 스트림은 Java의 컬렉션 데이터에 대해 SQL 질의문 처럼<br>
데이터를 처리할 수 있는 기능을 가지고 있습니다.<br>

## Stream이란?

### 기존 루프문 처리의 문제점

기존 Java에서 컬렉션 데이터를 처리할때는 for, foreach 루프문을 사용하면서 컬렉션 내의 요소들을
하나씩 다루었습니다. 간단한 처리나 컬렉션의 크기가 작으면 큰 문제가 아니지만 복잡한 처리가 필요하거나
컬렉션의 크기가 커지면 루프문의 사용은 성능저하를 일으키게 되었습니다.

### 스트림의 등장
스트림은 Java8에서 추가된 기능으로 컬렉션 데이터를 선언형으로 쉽게 처리할수 있습니다. 복잡한 루프문을

사용하지 않아도 되며 루프문을 중첩해서 사용해야 되는 최악의 경우도 더이상 없어졌습니다.

### 스트림의 특징
- 스트림은 데이터 소스로 부터 데이터를 읽기만 할 뿐, 데이터 소스를 변경하지 않는다.
- 스트림은 한번 사용하면 닫혀서 다시 사용할 수 없다.(다시 사용하려면 스트림을 다시 생성해야 한다.)

## 스트림 만들기

### 컬렉션

```
Stream<T> Collection.stream()
```

```
List<Integer> list = Arrays.asList(1,2,3,4,5);
Stream<Integer> intStream = list.stream();
intStream.forEach(i -> System.out.println(i));  // 또는 메서드 참조 방식으로 람다식 정의 intStream.forEach(System.out::println);
```


### 배열

```
Stream<T> Stream.of(T... values) // 가변인자
Stream<T> Stream.of(T[])
Stream<T> Arrays.stream(T[])
Stream<T> Arrays.stream(T[] array, int startInclusive, int endExclusive)  // startInclusive이상 endExclusive 미만 범위의 스트림 생성
```

```
사용 예)
Stream<String> strStream = Stream.of("a", "b", "c"); // 가변인자
Stream<String> strStream = Stream.of(new String[] {"a", "b", "c"});
Stream<String> strStream = Arrays.stream(new String[]{"a", "b","c"});
Stream<String> strStream = Arrays.stream(new String[]{"a", "b", "c", "d"}, 0, 3);
```

int, long, double과 같은 기본형 배열을 소스로 하는 스트림을 생성하는 메서드
```
IntStream IntStream.of(int... values)
IntStream IntStream.of(int[])
IntStream Arrays.stream(int[])
IntStream Arrays.stream(int[] array, int startInclusive, inbt endExclusive) // startInclusive이상 endExclusive 미만 범위의 스트림 생성
```
### 특정 범위의 정수
```
IntStream IntStream.range(int begin, int end)  // begin이상 ~ end 미만
IntStream IntStream.rangeClosed(int begin, int end) // begin 이상 ~ end 이하
```

### 임의의 수
Random 클래스에는 난수들로 이루어진 스트림을 반환하는 메서드를 가지고 있다.
```
IntStream ints()
LongStream longs()
DoubleStream doubles()
```
- 매개변수가 없다면 크키가 정해지지 않은 무한 스트림
- limit()를 함께 사용해서 스트림의 크기를 제한해 줘야 한다.
```
IntStream intStream = new Random().ints(); // 무한 스트림
intStream.limit(5).forEach(System.out::println); // 5개의 요소만 출력
```

- 매개변수가 있다면 크기가 정해진 유한스트림, limit()를 사용하지 않아도 된다.
```
IntStream ints(long streamSize)
LongStream longs(long streamSize)
DoubleStream doubles(long streamSize)
```

```
IntStream intStream = new Random().ints(5); // 크키가 5인 난수 스트림 반환
```

- 지정된 범위의 난수를 발생시키는 스트림을 얻는 메서드
```
begin이상 end 미만 범위에서 난수 발생
IntStream  ints(int begin, int end)
LongStream longs(long begin, long end)
DoubleStream doubles(double begin, double end)
IntStream ints(long streamSize, int begin, int end)
LongStream longs(long streamSize, long begin, long end)
DoubleStream doubles(long streamSize, double begin, double end)
```

### 람다식 - iterate(), generate()
람다식을 매개변수로 받아서 람다식에 의해 계산되는 값들을 요소로 하는 무한 스트림을 생성

```
static <T> Stream<T> iterate(T seed, UnaryOperator<T> f)
static<T> Stream<T> generate(Supplier<T> s)
```
- iterate()는 이전 결과를 이용해서 다음요소를 계산 
```
Stream<Integer> evenStream = Stream.iterate(0, n->n+2); // 0, 2, 4, 6 ... 
```

- generate()는 이전 결과를 사용하지 않고 람다식에 의해 계산되는 값을 요소로 하는 무한 스트림을 생성하여 반환
- generate()는 이전 결과를 사용하지 않으므로 매개변수 타입이 Suppiler<T> 이다. 

```
Stream<Double> randomStream = Stream.generate(Math::random);
Stream<Integer> oneStream = Stream.generate(() -> 1);
```

### 빈 스트림
- 요소가 하나도 없는 비어있는 스트림 
- 스트림에서 연산을 수행한 결과가 하나도 없을 때, null 보다 빈 스트림을 반환하는 것이 좋다.
```
Stream emptyStream = Stream.empty(); // 빈 스트림을 생성해서 반환 
long count = emptyStream.count(); // count의 값은 0
```

### 두 스트림의 연결 - concat()
```
String[] str1 = {"123", "456", "789"}
String[] str2 = {"ABC", "abc", "DEF"};
Stream<String> strs1 = Stream.of(str1);
Stream<String> strs2 = Stream.of(str2);
Stream<String> strs3 = Stream.concat(strs1, strs2); 
```

## 스트림의 중간 연산

### 스트림 자르기 - skip(), limit()
```
Stream<T> skip(long n)   // n만큼 건너뛰기
Stream<T> limit(long maxSize) // maxSize 만큼 자르기
```
```
IntStream intStream = IntStream.rangeClosed(1, 10); // 1~10의 요소를 가진 스트림
intStream.skip(3).limit(5).forEach(System.out::println); // 45678
```

### 스트림 요소 걸러내기 - filter(), distinct()
- filter() - 주어진 조건(Predicate)에 맞지 않는 요소를 걸러낸다.
- distinct() - 스트림에서 중복된 요소를 제거
```
Stream<T> filter(Predicate<? super T> predicate)
Stream<T> distinct()
```

- distinct() 
```
IntStream intStream = IntStream.of(1, 2, 2, 3, 3, 4, 5, 5, 6);
intStream.distinct().forEach(System.out::print); // 123456
```

- filter()
```
IntStream intStream = IntStream.rangeClosed(1, 10); // 1 ~ 10
IntStream.filter( i -> i % 2 == 0).forEach(System.out::print); // 246810
```

### 정렬 - sorted()
```
Stream<T> sorted()
Stream<T> sorted(Comparator<? super T> comparator)
```
Comparator를 지정하지 않으면 스트림 요소의 기본 정렬 기준(Comparable)으로 정렬한다. 단, 스트림의 요소가 Comparable을 구현한 클래스가 아니면 예외가 발생한다.

```
Stream<String> strStream = Stream.of("dd", "aaa", "CC", "cc", "b");
strStream.sort().forEach(System.out::println); 
```

#### Ex1_student
```java
package ex1_stream;

import java.util.ArrayList;
import java.util.Arrays;
import java.util.List;
import java.util.stream.IntStream;
import java.util.stream.Stream;

public class StudentMain {
	public static void main(String[] args) {
		List<Student> list = new ArrayList<>();
				list.add(new Student("홍길동",10));
				list.add(new Student("신용권",20));
				list.add(new Student("유미선",30));
				
		
		//방법1
		/*
		//student스트림
		Stream<Student> students = list.stream();
		
		//중간 처리(학생 객체를 점수로 매핑)
		//score스트림
		IntStream scoreStream = students.mapToInt(student -> student.getScore());
		
		//최종처리 (평균점수)
		double avg = scoreStream.average().getAsDouble();
		*/
		
		//방법2
		//.mapToInt() : 스트림을 IntStream으로 변환해주는 메서드
		//.average() : 요소의 평균 반환
		//.getAsDouble() : 최종 집계된 average의 값을 double형 변수에 넣기 위해 추출하는 메서드
		double avg = list.stream()
				.mapToInt(student -> student.getScore())
				.average()
				.getAsDouble();
		
		System.out.println("평균 점수 : " +avg);
		
	}
}
```






