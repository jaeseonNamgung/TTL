# HashMap vs LinkedHashMap

HashMap과 LikedHashMap에 가장 큰 차이점은 Key쌍을 매핑한 순서이다.

1. HashMap은 순서대로 저장되지 않는다.
2. LinkedHashMap은 순서대로 저장된다.

## 성능 차이

HashMap과 LinkedHashMap의 성능 차이는 크지 않다. Create 에서는 HashMap이 조금 더 빠르지만 Access 속도와 Iterate 속도는 LinkedHashMap이 더 빠르다.

![17367328759684481347426801984837.png](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Ft1.daumcdn.net%2Fcfile%2Ftistory%2F999B523D5D240E7A25)

# super()

1. 자신이 상속받은 부모 클래스에 레퍼런스 변수로 부모 클래스에 멤버 변수에 접근할 때 사용된다.
2. 자식 클래스에 생성자에서 부모 클래스에 생성자를 호출 할 때 사용된다.

    -  자식 클래스 생성자안에서 호출 할 때에는 코드 맨 윗줄에서 super() 키워드를 사용해야 된다.

# JDK 1.8

JDK 1.8 부터 함수형 프로그래밍 지원

- 람다식(Lambda expressions) - Stream
- 함수형 인터페이스 (Functional Interface)
- 디폴트 메서드 ( Default Method)
- JVM의 변화
- 병렬 배열 정렬(Parallel Array Sorting)
- 컬렉션을 위한 대용량 데이터 처리 ( 스트림 )
- Optional
- Base64 인코딩과 디코딩을 위한 표준 API
- 새로운 날짜, 시간 API (Date & Time API)

# trim() vs strip()

1. trim():
- `java.lang.String` 클래스의 `trim()` 메서드는 앞 뒤 공백을 모두 제거한 후 복사본을 리턴한다.
- `\u0020` 이하의 공백들만 제거된다.
1. strip():
- `java.lang.String` 클래스의 `strip()` 메서드는 java 11부터 나왔으며 마찬가지로 앞 뒤 공백을 모두 제거한다.
- 유니코드 공백을 모두 제거
- stripLeading(): 문자열 앞의 공백을 제거
- stripTrailing(): 문자열 뒤의 공백을 제거

# isEmpty vs isBlank

- isEmpty(): null 이거나 문자열의 길이가 0일 때
- isBlank():  공백으로만 되어 있는 문자열, 공백도 값이 없다고 판단 ( `trim().isEmtpy() == isBlank()` )

> `isBlank()`는 java11 부터 사용 가능

# static{} 대신 spring에서 대안

1. `@Valuue()` 또는 `@ConfigurationProperties` 사용: spring에서 정적으로 값을 초기화하는 대신 환경 변수나, `application.properties`로 값을 동적으로 값을 주입
2. 정적 변수를 사용해야 하는 경우 정적 변수를 직접 초기화 하지 않고 스프링 빈을 통해 값을 초기화
3. `@PostConstruct`를 통해 값을 초기화

> `@PostConstruct` 는 빈이 초기화 된 후 실행된다.
>

# Properties

`Properties` 는 java.util에서 제공하며, `FileInputStream` 으로 읽고 `load()` 메서드를 통해 해당 파일을 읽어 드린다.

```java
InputStream is = null;
// InputStream is = properties.class.getClassLoader().getResourceAsStream(fileName)도 가능
is = new FileInputStream("ws.properties");
p.load(is);
```

properties 파일이 load가 되면 `getProperties()` 메서드를 통해 key의 value에 접근할 수 있다.

```java
String gt = p.getProperty("key");
```

key의 추가나 수정은 `setProperties()` 로 가능하다.

```java
String gt = p.setProperty("key", "value");
```

> spring 에서는 `@Value()` 또는 `@ConfigurationProperties` 를 사용하면 될거 같다.
>

# getClass(), forName()

`getClass()` 와 `forName()`  메서드는 둘 다 클래스 정보를 얻기 위해 사용된다.

- getClass()

```java
package ClassGetName;
 
public class main {
 
	public static void main(String[] args) {
		Student student = new Student();
		//학생객체 생성
		System.out.println(student.getClass());
		
		Class clazz = student.getClass();
		//학생객체의 정보를 받는 클래스 객체 생성
		System.out.println(clazz.getName());
		System.out.println(clazz.getPackage().getName());
		System.out.println(clazz.getSimpleName());
	}
 
}
```

![image.png](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FkWdGk%2FbtqTKLI1b7I%2FwUKzjpk2WeB78IkKUCq5w1%2Fimg.png)

- forName()

```java
package ClassGetName;
 
public class main {
 
	public static void main(String[] args) {
 
 		System.out.println("____________클래스가 없을 경우를 대비한 try catch 문_______________");
		try {
			Class clazz2 = Class.forName("ClassGetName.Student");
			//존재하지 않을 클래스명을 입력하면 catch 문으로 이동한다.
			System.out.println(clazz2.getName());
			System.out.println(clazz2.getPackage().getName());
			System.out.println(clazz2.getSimpleName());
		}catch (ClassNotFoundException e) {
			e.printStackTrace();
		}
	
	}
 
}
```

Student 객체를 생성하지 않고 클래스 정보를 확인 할 경우에는 `forName()` 메서드를 사용하면 된다.  forName() 메서드 안에는 `패키지.클래스` 이름을 적어주면 된다.  단 클래스가 존재하지 않을 경우 `ClassNotFoundException` 예외가 발생하기 때문에 `try/catch` 문으로 예외를 대비해야 한다.

# Log 레벨

1. debug: 개발 혹은 테스트 단계에서 해당 기능들이 정상적으로 동작 하는지를 확인하기 위한 로그 레벨
2. info: 애플리케이션에서 정상 작동에 대한 정보, 즉 어떤 일이 발생했음을 나타내는 표준 로그 레벨
3. warn: 애플리케이션에서 잠재적으로 문제가 될 수 있는 상황일 때 나타내는 로그 레벨
4. error: 애플리케이션에서 심각한 에러나 예외 상황일 때 나타내는 로그 레벨

> 로그 레벨 중 WARN과 ERROR을 구분하면 진짜 봐야할 중요한 문제들만 볼 수 있다.
둘의 레벨을 구분하면 아래와 같이 모니터링 기준을 가져갈 수 있다.
>
>
> INFO: 기존대비 +-50%이상 차이날 경우 알람
> WARN: 분당 20개이상일 경우 알람
> ERROR: 분당 5개이상일 경우 알람
>
