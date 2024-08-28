# 스프링 예외 처리과정
## 과정
1. 컨트롤러 이하 모듈에서 예외가 발생하면 WAS까지 올라간다
2. WAS는 어플리케이션에서 처리하지 못하는 예외라고 판단하고 예외 대응을 수행
3. 스프링부트는 기본적으로 예외가 발생하면 BasicErrorController로 핸들링(스프링부트 자동구성에 의해 설정)

## BasicErrorController
````java
@Controller
@RequestMapping("${server.error.path:${error.path:/error}}")
public class BasicErrorController extends AbstractErrorController {

    private final ErrorProperties errorProperties;
    ...

    @RequestMapping(produces = MediaType.TEXT_HTML_VALUE)
    public ModelAndView errorHtml(HttpServletRequest request, HttpServletResponse response) {
        ...
    }

    @RequestMapping
    public ResponseEntity<Map<String, Object>> error(HttpServletRequest request) {
        ...
        return new ResponseEntity<>(body, status);
    }
    
    ...
}
````
errorHtml()과 error()는 모두 getErrorAttributeOptions를 호출해 반환할 에러 속성을 얻는데,
기본적으로 DefaultErrorAttributes로부터 반환할 정보를 가져온다. DefaultErrorAttributes는 전체 항목들에서 설정에 맞게 불필요한 속성들을 제거한다.
### 한계
`BasicErrorController`에서 제공하는 정보들이 클라이언트 입장에서 유용하지 못하다.
```java
{
    "timestamp": "2021-12-31T03:35:44.675+00:00",
    "status": 500,
    "error": "Internal Server Error",
    "path": "/product/5000"
}
```
사용자는 클라이언트가 필요한 에러코드와 메시지 등 담는 하나의 예외처리 전략이 필요하다.

## ExceptionHandler
* 추상화된 예외처리 전략(전략 패턴)
* 컨트롤러 내 메소드 혹은 `@ControllerAdvice`가 붙은 클래스 내 메소드에 사용 가능
* 기존의 `@ResponseStatus` 나 `ResponseStatusException`가 하지 못한 payload 설정 가능
* 유연한 응답 형식 가능

## ControllerAdvice
### RestControllerAdvice vs ControllerAdvice
`RestControllerAdvice`는 ResponseBody 형태의 응답(json), ControllerAdvice는 html 형태의 응답

* 여러 핸들러에서 발생한 예외에 대한 전역적인 처리를 담당한다
* 예외 응답의 일관된 처리가 가능하다

### ResponseEntityExceptionHandler 상속
스프링 기본 예외들 같은 경우 `RestControllerAdvice`에 정의되어 있지 않은 경우 `DefaultHandlerExceptionResolver`가 동작하게 되는데
이러면 일관된 예외 응답 처리를 하지 못하게 된다. 따라서 스프링 기본 예외 처리에 대한 추상 클래스인 `ResponseEntityExceptionHandler`를 상속받자.
하지만 이 또한 메시지를 기본적으로 반환하지 않으므로 오버라이딩이 필요하다. 
**이를 통해 사용자 정의 예외를 제외한 스프링 예외에 대한 일괄 처리가 가능하다.**

### 스프링 예외처리 흐름
![스프링 예외처리 흐름](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FtLgqM%2FbtrpKDUUdG2%2FoJayCyPYGAcdpPAPQNBe30%2Fimg.png)
1. 컨트롤러 내 `@ExceptionHandler`
2. `@ControllerAdvice` 내 `@ExceptionHandler`
3. 발생한 예외가 `@ResponseStatus` 처리 여부
4. 스프링 내부 기본 예외들을 처리하는 DefaultHandlerExceptionResolver가 동작
5. 적합한 ExceptionResolver를 찾지 못한 경우 BasicErrorController 호출

## 참고 자료
* [스프링의 다양한 예외 처리 방법 완벽 이해하기](https://mangkyu.tistory.com/204)
* [@RestControllerAdvice를 이용한 Spring 예외 처리 방법](https://mangkyu.tistory.com/205)