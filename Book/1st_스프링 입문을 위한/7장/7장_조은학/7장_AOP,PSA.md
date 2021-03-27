아래 글의 더 자세한 내용은
https://durumiss.tistory.com/6 에서 확인하실 수 있습니다.


## **AOP**

스프링 DI 가 의존성(new) 에 대한 주입이라면

스프링 AOP 는 로직(code) 주입이라고 볼 수 있다.

프로그램에서 다수의 묘듈에 공통적으로 나타나는 부분이 존재한다는 것을 횡단 관심사라고 한다.

로직을 어디에 주입할까?

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbX1qhK%2Fbtq08ugQjI8%2FWWeBkZeWdFkmiFXuinkWa1%2Fimg.png)

이렇게 5군데에 집어 넣을 수 있다.

AOP를 위한 소스코드 전후의 모습이다

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcgdQE2%2Fbtq090sh3JS%2FOkvVIKPuCZ7YMOlL2SjHqk%2Fimg.png)

‘횡단 관심사’를 지우고 단순해진 모습이다

이렇게 함으로써 boy.java파일에는 횡단관심사는 사라지고 핵심관심사만 남았다

프록시 패턴을 이용해 횡단 관심사를 핵심 관심사에 주입하는 것이다.

(SRP를 적용한 것으로도 볼 수 있다.)

SRP란

SRP 단일책임원칙

한클래스는 하나의 책임만 가져야한다는 원칙이다.

아래는 AOP적용 전 후 의 전체 코드이다.

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcyhL1y%2Fbtq091x0z4n%2F18BDy3GG9frlAKcNNMeUm1%2Fimg.png)

프록시를 이용해 runSomething 메소드를 호출하는 모습이다.

스프링 AOP의 핵심

1\. 스프링 AOP는 인터페이스 기반이다.

2\. 스프링 AOP는 프록시 기반이다.

3\. 스프링 AOP는 런타임 기반이다.

스프링 AOP에서의 용어

1\. Aspect 

2\. Advisor

3\. Advice

4\. JoinPoint

5\. Pointcut

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fcrhhbr%2Fbtq1b9oiGal%2F6iqa4iNcfYk0DyekP47bzk%2Fimg.png)

5\. Pointcut

Aspect적용 위치 지정자이다.

@Before는 before메소드가 runSomething 메서드 실행하기 전에 실행하라는 의미이다.

4\. JoinPoint

Aspect적용이 가능한 모든 지점을 지칭한다.

좁은의미에서의 JoinPoint는 호출된 객체의 메서드다.

3\. Advice

pointcut에 적용할 로직, 즉 메서드를 의미한다.

여기에 언제라는 개념까지 포함한다.

before메서드를 의미한다

2\. Aspect

Aspect=Advice+Pointcut이다.

1\. Advisor

Advisor=한 개의 Advice+ 한 개의 Pointcut이다.

## **PSA**

PSA 일관성 있는 서비스 추상화이다.

서비스 추상화는 같은 일을 하는 다수의 기술을 공통의 인터페이스로 제어할 수 있게 한 것이다.

스프링은 다양한 기술(ORM, 캐시, 트랜잭션) 등에 대한 PSA를 제공한다.

코드, 이미지 출처 : [github.com/expert0226/oopinspring](https://github.com/expert0226/oopinspring)
