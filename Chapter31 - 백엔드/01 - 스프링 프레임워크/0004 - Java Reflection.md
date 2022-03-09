## Java Reflection



- 정적 언어는 컴파일시 미리 파악, 객체 생성들을 해두어야 하지만.. 동적 언어처럼 런타임시에 객체 정보를 파악해 생성할 수 있게 서포트 해주는 듯. 
  - IDE에서 개발자가 간단히 클래스의 메소드나 정보를 파악할 수 있는것도 리플렉션 기능 덕분?
- 런타임시에는 JVM의 힙(?) 메모리에 로드된 클래스에 리플렉션을 통해 접근해서 정보를 파악, 수정, 메소드 호출등이 가능
- 접근 제한자에 상관 없이 정보를 가져올 수도 있기 때문에 사용에 주의가 필요.






https://lob-dev.tistory.com/entry/Java%EC%9D%98-Reflection-API

https://kmongcom.wordpress.com/2014/03/15/%EC%9E%90%EB%B0%94-%EB%A6%AC%ED%94%8C%EB%A0%89%EC%85%98%EC%97%90-%EB%8C%80%ED%95%9C-%EC%98%A4%ED%95%B4%EC%99%80-%EC%A7%84%EC%8B%A4/

https://velog.io/@guswns3371/%EB%A6%AC%ED%94%8C%EB%A0%89%EC%85%98







```java
	@Test
	void test01() throws ReflectiveOperationException {

//		Class<?> bookClass = Class.forName("com.reflection.demo.entity.Book");
		Class<?> bookClass = Class.forName("Book");
		Constructor<?> bookConstructor = bookClass.getConstructor(String.class, LocalDate.class);
		Object bookInstance = bookConstructor.newInstance("testBook", LocalDate.of(2020, 1, 1));
		System.out.println(bookInstance);
		
		Book book = (Book) bookInstance;
		book.setYear(LocalDate.of(2022, 12, 30));
		System.out.println(bookInstance);
		
		System.out.println("end");

	}
```
```java
	@Test
	void test02() throws ReflectiveOperationException {

		Reflections reflections = new Reflections("com.reflection.demo.entity"); // 패키지 스캔
		Class<?> testClass = reflections.getClass();
		Constructor<?> testConstructor = testClass.getConstructor(String.class, LocalDate.class);
		Object testInstance = testConstructor.newInstance("testBook2", LocalDate.now());
		System.out.println(testInstance);
	}
```