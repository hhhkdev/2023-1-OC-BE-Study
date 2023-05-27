# 8주차

**학습 범위 : 스프링 입문을 위한 자바 객체 지향의 원리와 이해 챕터 7**

****2023년 5월 29일 00시 까지****

**[필수 정리 내용]**

1) **IoC와 프레임 워크, 라이브러리**

2) **생성자를 통한 의존성 주입과 @Autowired 비교**

3) **AOP**

**[선택 정리 내용]**

1.

보기처럼 의존성 주입을 할 때, (1)~(3)의 질문에 답하시오.

(보기)

[https://oopy.lazyrockets.com/api/v2/notion/image?src=https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F76d1052a-d9cc-47e2-8b91-e0002483686b%2FUntitled.png&blockId=b91c957f-cea4-43b4-876f-930ca91e9885](https://oopy.lazyrockets.com/api/v2/notion/image?src=https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F76d1052a-d9cc-47e2-8b91-e0002483686b%2FUntitled.png&blockId=b91c957f-cea4-43b4-876f-930ca91e9885)

(1) 의존성 주입 방법에는 어떤 것이 있는지 기재하시오.

(2) 여러 의존성 주입 방법중에 private final 문법과 @RequiredArgsConstructor 어노테이션을 사용하여 주입 하는 이점이 무엇일지 쓰시오.
(3) @AllArgsConstructor, @NoArgsConstructor는 무엇인지 쓰시오.

2.

AOP를 이용하여 많은 기능을 구현할 수 있다. 대표적인 것을 조사하고 정리하시오.

---

# POJO

**Plain Old Java Object**

스프링을 이해하는 데는 **스프링 삼각형**(IoC/DI, AOP, PSA)라고 하는 스프링의 3대 프로그래밍 모델에 대한 이해가 필요함.

스프링 프레임워크와 스프링 삼각형의 관계는 **영어 문장과 알파벳의 관계**.

# IoC/DI - 제어의 역전/의존성 주입

**IoC**(Inversion of Control / 제어의 역전), **DI**(Dependency Injection / 의존성 주입)

전체가 부분에 의존, “프로그래밍에서 의존 관계는 new로 표현됨.

## 의존성 주입 (생성자)

- 의사 코드
    - 운전자가 타이어를 생산한다.
    - 운전자가 자동차를 생산하면서 타이어를 장착한다.

### ex)

의존성 주입을 적용할 경우, Car 객체는 그저 Tire 인터페이스를 구현한 어떤 객체가 들어오기만 하면 정상적으로 작동함.

**의존성 주입을 하면 확장성도 좋아짐** → 나중에 다른 타이어 브랜드가 들어오더라도 [`Car.java`](http://Car.java) 코드를 변경할 필요없이 사용할 수 있음.

⇒ 추후 코드를 재배포할 필요가 없도록 구성해야만 코드 재컴파일과 재배포에 대한 부담을 덜 수 있음. 인터페이스를 구현했기에 얻는 이점.

**전략 패턴의 3요소**: `클라이언트`, `전략`, `컨텍스트`

⇒ 전략 메소드를 가진 전략 객체, 전략 객체를 사용하는 컨텍스트, 전략 객체를 생성해 컨텍스트에 주입하는 클라이언트(제3자)

### ex)

전략: `Tire`를 구현한 `KoreaTire, AmericaTire`

컨텍스트: `Car`의 `getTireBrand()` 메소드

클라이언트: `Driver`의 `main()` 메소드

## 의존성 주입 (속성)

최근에는 생성자를 통한 의존성 주입을 선호함.

- 의사 코드
    - 운전자가 타이어를 생산한다.
    - 운전자가 자동차를 생산한다.
    - 운전자가 자동차에 타이어를 장착한다.

## 스프링을 통한 의존성 주입 (`XML` 파일)

- 의사 코드
    - 운전자가 종합 쇼핑몰에서 타이어를 구매한다.
    - 운전자가 종합 쇼핑몰에서 자동차를 구매한다.
    - 운전자가 자동차에 타이어를 장착한다.

스프링을 도입해서 얻는 이득:

자동차의 타이어 브랜드를 변경할 때 그 무엇도 재컴파일/재배포하지 않아도 XML 파일만 수정하면 프로그램의 실행 결과를 바꿀 수 있음.

## 스프링을 통한 의존성 주입 (스프링 설정 파일 (`XML`)에서 속성 주입)

`XML` 파일의 `property` 태그를 이용함. 

## 스프링을 통한 의존성 주입 - `@Autowired`를 통한 속성 주입

- 의사 코드
    - 운전자가 종합 쇼핑몰에서 자동차를 구매 요청한다.
    - 종합 쇼핑몰은 자동차를 생산한다.
    - 종합 쇼핑몰은 타이어를 생산한다.
    - 종합 쇼핑몰은 자동차에 타이어를 장착한다.
    - 종합 쇼핑몰은 운전자에게 자동차를 전달한다.

`import`문 하나와 `@Autowired` 애노테이션을 이용하면 설정자 메소드를 이용하지 않고도 스프링 프레임워크(종합쇼핑몰)가 설정 파일을 통해 설정자 메소드 대신 속성을 주입해 줌.

`@Autowired`의 의미: 스프링 설정 파일을 보고 자동으로 속성의 설정자 메소드에 해당하는 역할을 해주겠다는 의미.

스프링의 @Autowired - type 기준 매칭: 같은 타입을 구현한 클래스가 여러 개 있다면 그때 bean 태그의 id로 구분해서 매칭하게 되는 것.

## 스프링을 통한 의존성 주입 - `@Resource`를 통한 속성 주입

- 의사 코드
    - 운전자가 종합 쇼핑몰에서 자동차를 구매 요청한다.
    - 종합 쇼핑몰은 자동차를 생산한다.
    - 종합 쇼핑몰은 타이어를 생산한다.
    - 종합 쇼핑몰은 자동차에 타이어를 장착한다.
    - 종합 쇼핑몰은 운전자에게 자동차를 전달한다.

`@Autowired`는 스프링의 어노테이션, `@Resource`는 **자바 표준 어노테이션**.

`@Autowired`의 경우, `type`과 `id` 가운데 매칭 우선순위는 `type`이 높음. `@Resource`의 경우는 `id`가 높음.

⇒ `@Resource`의 경우 `id`로 매칭할 빈을 찾지 못한 경우, `type`으로 매칭할 빈을 찾음.

## 스프링을 통한 의존성 주입 - `@Autowired` vs. `@Resource` vs. `<property>` 태그

|  | @Autowired | @Resource |
| --- | --- | --- |
| 출처 | 스프링 프레임워크 | 표준 자바 |
| 소속 패키지 | org.springframework.beans.factory.annotation.Autowired | javax.annotation.Resource |
| 빈 검색 방식 | byType 먼저, 못 찾으면 byName | byName 먼저, 못 찾으면 byType |
| 특이사항 | @Qualifier(””) 협업 | name 어트리뷰트 |
| byName 강제하기 | @Autowired
@Qualifier(”tire1”) | @Resource(name=”tire1”) |

# AOP

**Aspect-Oriented Programming** 관점 지향 프로그래밍

> 스프링 DI가 의존성에 대한 주입이라면 스프링 AOP는 **로직 주입**이라고 볼 수 있다.
> 

- `@Aspect`는 이 클래스를 이제 AOP에서 사용하겠다는 의미다.
- `@Before`는 대상 메소드 실행 전에 이 메소드를 실행하겠다는 의미다.

⇒ 스프링 AOP는 인터페이스 기반, 프록시 기반, 런타임 기반이다.

스프링 AOP에서 `JoinPoint`란 스프링 프레임워크가 관리하는 빈의 모든 메소드에 해당함. 

광의의 JoinPoint: Aspect 적용이 가능한 모든 지점 / 협의의 JoinPoint: 호출된 객체의 메소드

### Advice

Pointcut에 적용할 로직, 메소드를 의미함. 여기에 언제라는 개념이 포함됨.

즉, Pointcut에 언제, 무엇을 적용할지 정의한 메소드. (타깃 객체의 타깃 메소드에 적용될 부가 기능)

### Aspect

여러 개의 Advice와 여러 개의 Pointcut의 결합체를 의미하는 용어. When + Where + What

# PSA

**Portable Service Abstration** 일관성 있는 서비스 추상화.

**어댑터 패턴**을 적용해 같은 일을 하는 다수의 기술을 공통의 인터페이스로 제어할 수 있게 한 것.

**OXM 기술**(Object XML Mapping: 객체와 XML 매핑): Castor, JAXB, XMLBeans, JiBX, XStream 등

⇒ 어댑터를 통해 일관된 방식으로 코드를 작성할 수 있도록 해줌.