# Composite 패턴
## 개요
Composite 패턴은 구조적 디자인 패턴 중 하나로, 개별 객체와 복합 객체를 동일하게 다룰 수 있도록 설계하는 방법이다.
이 패턴은 객체들이 트리 구조를 이루고 있을 때 유용하며, 클라이언트가 단일 객체와 복합 객체를 구분하지 않고 일관되게 처리할 수 있게 한다.
예를 들어, 단일 파일과 폴더 내의 파일들을 동일한 방식으로 접근할 수 있게 해준다.

## 구성
Composite 패턴은 `Component`, `Leaf`, `Composite` 세 가지 주요 요소로 구성된다.
`Component`는 객체들의 공통 인터페이스를 정의하는 역할을 한다. `Leaf`는 트리 구조의 말단을 이루는 개별 객체를 나타내며, 실제 작업을 수행한다.
`Composite`는 다른 `Component`들을 자식으로 가지며, 자식들을 관리하고 작업을 위임하는 역할을 한다.

## 장점
이 패턴의 장점은 트리 구조의 유연한 관리와 재사용성에 있다. 클라이언트 코드가 단일 객체와 복합 객체를 구분하지 않고 처리할 수 있기 때문에 코드가 단순해지고 유지보수가 용이해진다.
또한, 새로운 유형의 객체를 추가할 때도 기존 코드를 크게 수정할 필요가 없다.(OCP를 위배하지 않는다.)

## 단점
하지만 Composite 패턴을 사용할 때는 트리 구조의 복잡성이 증가할 수 있으며, 전체 구조를 이해하고 관리하는 데 어려움이 있을 수 있다.
또한, 디버깅과 인터페이스 설계가 어렵다는 단점이 존재한다.

## 사용하는 조건
1. 모든 원소들을 순회하면서 수행하길 바랄 때(재귀를 통해)
2. 하나 이상의 원소를 한번에 추가, 삭제를 하고 싶을 때

## Spring에서 사용하는 Composite 패턴
### 1. WebMvcConfigurerComposite
* `WebMvcConfigurer`를 `Component`로 하여 하위의 모든 `Component`에 대한 설정을 해주어야 하기 때문에 사용
* 조건 1, 2를 모두 만족한다
### 2. HandlerExceptionResolverComposite
* `HandlerExceptionResolver`가 `Component`
* 모든 `HandlerExceptionResolver`를 순회하며 예외 처리 가능여부를 확인한다
### 3. ViewResolverComposite
* `ViewResolver`가 `Component`
* 모든 `ViewResolver`를 순회하며 뷰 템플릿으로 사용 가능여부를 확인한다
### 4. HandlerMethodArgumentResolverComposite and else...

## 출처
* [복합체(Composite) 패턴 - 완벽 마스터하기](https://inpa.tistory.com/entry/GOF-%F0%9F%92%A0-%EB%B3%B5%ED%95%A9%EC%B2%B4Composite-%ED%8C%A8%ED%84%B4-%EC%99%84%EB%B2%BD-%EB%A7%88%EC%8A%A4%ED%84%B0%ED%95%98%EA%B8%B0)
* [SpringBoot 소스 분석하기](https://mangkyu.tistory.com/216)
