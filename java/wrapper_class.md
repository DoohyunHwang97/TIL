# 자바 Wrapper 클래스

자바의 Wrapper 클래스는 기본 자료형(primitive type)을 객체로 다룰 수 있도록 해주는 클래스이다. Wrapper 클래스는 자바의 기본 자료형을 감싸 객체로 만들어 주며, 이로 인해 객체가 필요한 곳에서 기본 자료형을 사용할 수 있다.

## 기본 자료형과 대응되는 Wrapper 클래스

| 기본 자료형 | Wrapper 클래스 |
| ----------- | -------------- |
| `boolean`   | `Boolean`      |
| `byte`      | `Byte`         |
| `char`      | `Character`    |
| `short`     | `Short`        |
| `int`       | `Integer`      |
| `long`      | `Long`         |
| `float`     | `Float`        |
| `double`    | `Double`       |

## 주요 특징

### 1. 자동 박싱(Auto Boxing) 및 언박싱(Unboxing)
- **자동 박싱**: 기본 자료형이 자동으로 그에 대응하는 Wrapper 객체로 변환되는 것이다.
  ```java
  Integer num = 10;  // int가 Integer로 자동 변환
* 언박싱: Wrapper 객체가 자동으로 기본 자료형으로 변환되는 것이다.
    ```java
    int n = num;  // Integer가 int로 자동 변환
    ```
### 2. 캐싱(Caching)
자바는 성능 향상을 위해 특정 범위의 값을 캐싱한다. 캐싱된 값은 동일한 객체를 재사용하므로 메모리 효율을 높일 수 있다.

* Integer, Byte, Short, Long, Character:
  - 128에서 127까지의 값은 캐싱된다.
  - 예시:
    ```
    Integer a = Integer.valueOf(127);
    Integer b = Integer.valueOf(127);
    System.out.println(a == b); // true (캐싱된 객체 재사용)
    ```
* Boolean:
  - Boolean.TRUE와 Boolean.FALSE 두 가지 값만 캐싱된다.
  - 예시:
      ```
      Boolean t1 = Boolean.valueOf(true);
      Boolean t2 = Boolean.valueOf(true);
      System.out.println(t1 == t2); // true (캐싱된 객체 재사용)
      ```
### 3. 메모리 사용
   각 Wrapper 객체는 기본 자료형을 포함한 추가 메모리를 사용한다.

* 객체 헤더(Object Header): 일반적으로 12바이트(64비트 JVM, OpenJDK 8 기준).
* 값(Value): 기본 자료형에 따라 다르다 (예: Integer는 4바이트, Long은 8바이트).
* 패딩(Padding): 객체 크기를 8바이트 단위로 정렬하기 위한 패딩이 추가된다.(64비트 CPU)

예를 들어, new Long(1)의 경우, 일반적인 64비트 JVM에서 12바이트의 객체 헤더와 8바이트의 long 값, 그리고 4바이트의 패딩으로 총 24바이트를 차지한다.

### 4. 성능 고려사항
   캐싱 범위 내의 값: valueOf() 메서드를 사용하여 객체를 생성하면 캐싱된 객체를 재사용하므로 메모리와 성능에 유리하다.
   캐싱 범위 외의 값: new 키워드를 사용하여 객체를 생성하면 매번 새로운 객체가 생성된다. 이는 메모리와 성능에 불리할 수 있다.
### 5. 사용 권장사항
   기본 자료형을 가능한 많이 사용하고, 객체로서의 필요성이 있을 때만 Wrapper 클래스를 사용한다.
   다만 자주 사용되는 값들은 Wrapper 클래스의 캐싱을 적극 활용하자.
   객체 생성 시 new 키워드보다는 valueOf() 메서드를 사용하는 것이 메모리 사용을 줄이고 성능을 향상시킬 수 있다.
   
## 참고자료
* [java가 메모리를 할당하는 방법](https://tangoblog.tistory.com/14)
* [Integer 캐시](https://mangkyu.tistory.com/273)
* [FlyWeight 패턴](https://inpa.tistory.com/entry/GOF-%F0%9F%92%A0-Flyweight-%ED%8C%A8%ED%84%B4-%EC%A0%9C%EB%8C%80%EB%A1%9C-%EB%B0%B0%EC%9B%8C%EB%B3%B4%EC%9E%90)