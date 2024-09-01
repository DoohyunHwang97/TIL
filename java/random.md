# 자바에서의 난수 생성
* 크게 java.util.Random 과 java.lang.Math의 random 메소드를 사용할 수 있다.
* 난수를 생성하기 어려운 컴퓨터 특성상 종자값을 정해줘야 하는데 Math.random의 경우 System.currentTimeMillis를 종자값으로 사용한다
* Random 클래스는 객체를 생성할 때 종자값 설정이 가능하다. 하지만 특정한 값으로 설정할 경우 종자값에 의존하는 난수 알고리즘의 특성에 따라 정해진 패턴으로 난수가 생성된다.

```java
public Random() {
        this(seedUniquifier() ^ System.nanoTime());
    }
```

## 사용법
### Random 클래스
```java
random.nextInt(4); // 0 ~ 3 까지의 무작위 int 값 리턴
random.nextInt(10); // 0 ~ 9 까지의 무작위 int 값 리턴 
random.nextInt(100); // 0 ~ 99 까지의 무작위 int 값 리턴 

random.nextInt(4)+1; // 1 ~ 4 까지의 무작위 int 값 리턴 
random.nextInt(4)+100; // 101 ~ 104 까지의 무작위 int 값 리턴
```

### Math.random
```java
Math.random();
```
* 0.0 ~ 1.0 사이의 난수가 1개 발생한다.
```java
(int)(Math.random()*10); //0 ~ 10 사이
(int)(Math.random()*100); // 0 ~ 100 사이

(int)(Math.random()*10+10)); //10 ~ 20 사이
```