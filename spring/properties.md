# 스프링 전역변수 활용법
## @Value
* 런타임에 표현식을 기반으로 값을 주입
* **설정의 분리**
* Spring Batch의 Late Binding에 사용
## SPEL
## Placeholder Expression
### 문법
* `${propertyName:defaultValue}`
* nested 형태도 가능하다
```java
@Controller
@RequestMapping("${server.error.path:${error.path:/error}}")
public class BasicErrorController extends AbstractErrorController {
    ...
}
```
server.error.path -> error.path -> /error 순으로 찾는다.

## 참조
* [@Value 애노테이션의 역할과 기능](https://catsbi.oopy.io/379afd0c-d956-4133-b585-20d13d823c1a)
* [Spring Batch 가이드](https://jojoldu.tistory.com/330)
* [Spring Boot에서 properties 값 주입받기](https://tecoble.techcourse.co.kr/post/2020-09-29-spring-properties-binding/)