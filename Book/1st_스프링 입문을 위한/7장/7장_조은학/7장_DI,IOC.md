아래 글의 더 자세한 내용은
https://durumiss.tistory.com/5 에서 확인하실 수 있습니다.

## **IoC/DI**

**의존이란?**

운전자가 자동차를 생산한다

자동차는 내부적으로 타이어를 생산한다.

이것을 자바 코드로 표현하면

new Car();

Car 객체 생성자에서 new Tire();

로 표현할 수 있다.

이것을 car가 tire에 의존한다고 한다.

또한 프로그래밍에서의 의존 관계는 new로 표현된다고 할 수 있다. 

**기존의 주입 방식**

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Ftzptg%2Fbtq09zIrGXL%2FgfJAnDyRDDH6j0txW2SMkk%2Fimg.png)

자동차는 타이어에 의존한다

운전자는 자동차를 사용한다

운전자가 자동차에 의존한다고 볼 수 있다.

자동차의 생성자 코드에서 tire 속성에 새로운 타이어를 생성해서 참조할 수 있게 해주었다.

**1\. 스프링 없이 의존성 주입**

(1) 생성자를 통해 주입

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbjZYfP%2Fbtq1atufBIT%2FEgnnMTeYdHcMqfio0pTTAk%2Fimg.png)

new를 통해 타이어를 생산하는 부분이 car.java에서 driver.java로 이동하였다.

어떤 타이어를 생산해서 장착할까를

자동차가 고민하지 않고 운전자가 고민한다!

이 방식의 이점:

1\. 기존 방식에서는 car가 tire가 어떤 브랜드인지 정확히 알고있어야만 하는데 이 방식에서는 car는 tire가 다른 브랜드가 생겨도 car는 상관없이 사용할 수 있다.

(2) 속성을 통해 주입

(1)의 방식에서는 ‘생산’할 때 한번 타이어를 장착하면 더이상 타이어를 교체할 방법이 없다!

운전자가 원할때 car의 tire을 교체할수 있게하려면 생성자가 아닌 속성을 통한 의존성 주입이 필요하다

but 실무에서는 생성자를 통한 의존성 주입을 선호하는 사람이 많다고 한다

**2\. 스프링을 통한 의존성 주입**

(1) xml 사용(속성을 통해 주입한 방법임)

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdZHCCl%2Fbtq09x4VuV9%2F7lGkaIDU1tn1tK4GFI0A20%2Fimg.png)

\-->종합 쇼핑몰에서 상품에 해당하는 car와 tire을 구매하는 코드라고 보면 된다

종합쇼핑몰에 입점은 xml파일에서 한다

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcCOiNf%2Fbtq09Z7X3LR%2FhTrGhdFAHMkRBZkimjuKp0%2Fimg.png)

여기서 스프링의 이점?

\-->자동차의 타이어 브랜드를 변경할 때 그 무엇도 재컴파일/재배포 하지 않고 xml만 수정하면 된다!

(2) xml에서 속성을 주입해버리기

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FrfFtI%2Fbtq1caOfSxB%2FkpEPBMGNGZXfeo15LRw660%2Fimg.png)

차 안에 property로 tire가 있다!

(3) Autowired 사용

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbvYqvD%2Fbtq08uuhUxX%2FkSQR3e7j7X2BKffScVXkDk%2Fimg.png)

car.java에서 위의 코드가 아래의 코드로 변경되었다

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fbk3QCr%2Fbtq1bfWyzFt%2F5HanKvt3MMLHLlSs7lMbfK%2Fimg.png)

xml파일에서도 @Autowird 를 통해서 자동으로 car 의 property 를 찾아줄 수 있음으로 생략이 가능해졌다.

xml을 사용할 때 Spring은type 기준 매핑이 먼저이고, 같은 type을 구현한 여러 개의 클래스가 있다면 그 때 bean id 로 구분해서 매핑하게 된다.

즉, type 다음에 id로 매핑이 이루어진다.

(4) Resource 사용

@Autowired가 @Resource로 변경됨

@Autowired-스프링 어노테이션

@Resource-자바 표준 어노테이션!!

XML 설정 사용

장점 : XML을 사용하면 컴파일 없이 빈 설정 정보를 변경할 수 있다

하지만 최근에는 거의 XML 기반의 설정은 사용하지 않는다

(김영한 강사님 스프링 핵심 원리 출처)
