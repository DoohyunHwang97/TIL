# 어노테이션

## 정의
프로그램에게 제공하는 메타 데이터

## 용도
- 프로그램에 정보 제공
- 컴파일러에 정보 제공하여 추가적인 코드 생성
- 런타임에 특정 기능 실행 처리

## 표준 어노테이션
- @Override
- @Deprecated
- @SuppressWarning
- @FunctionalInterface

## 메타 어노테이션
- @Target(ElementType.METHOD)
- @Rentention(RetentionPolicy.RUNTIME)
- @Documented
- @Inherited

## 문법
- 어노테이션 내에 함수 정의 가능

    ```java
    public @interface annotation
    ```
- 필드 값 지정가능 → Reflection 통해서 정보 얻을 수 있음
```java
public @interface MyAnnotation {
	public int number();
	public String text();
}

@MyAnnotation(number=1, text="one")
public class Client {
}
```