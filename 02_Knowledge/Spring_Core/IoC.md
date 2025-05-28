# IoC (Inversion of Controll)

## 🔍  정의

IoC 는 객체 생성 및 생명주기 관리를 개발자가 아닌, 프레임워크가 담당하는 개념이다.

## **Spring IoC** : Spring Container

그렇다면 스프링은 어떻게 객체를 생성하고 주입할 수 있게 해주는 것인가?

결론부터 말하자면, **Spring Container 라는 녀석이 [[02_Knowledge/Spring_Core/자동 구성.md|'객체 정의'를 미리 읽고]], 그 정의를 기반으로 객체를 생성하고, 의존성을 주입하며, 생성주기를 관리한다.**

주로 **ApplicationContext** 를 이용해서 구현하는데, Bean Factory, IoC Container, Spring Container 등 여러 방법으로 불러질 수 있지만 모두 비슷한 개념으로 보면 된다.

이전에 서블릿을 통해 Context 에 대한 개념을 이해할 수 있었다. 그렇다면, 스프링에서도 Context(환경) 에서 객체를 관리하는 구조라는 것을 알 수 있다.

---
##  🔧 예시

```java
public class Communication implements Steps {
	private final Greeting greeting;
	private final Farewell farewell;
	private final Sender sender;

	public Communication() {
		this.greeting = new EnglishGreeting();
		this.farewell = new EnglishFarewell();
		this.sender = new ConsoleSender();
	}

	// ...
	
}
```

위 코드에서 각 구현체 클래스들을 다른 클래스로 수정하고 싶으면 어떻게 해야할까?

```java
public Communication() { 
	this.greeting = new KoreanGreeting(); 
	this.farewell = new EnglishFarewell(); 
	this.sender = new ConsoleSender(); 
}
```

물론 위처럼 쉽게 수정할 수 있다.

그러나, 이 ``communication()`` 과 같은 클래스가 많아진다면, 일일이 다 하나씩 수정해줘야 한다는 불편함이 생긴다.

**이 과정을 개발자가 하지않게 프레임워크가 대신 하는 것을 IoC** 라 하고, 스프링에서는 이를 **@Autowired** 나 **@Component** 같은 **의존성주입(DI)** 으로 해결한다.

---
## 🔗  관련

- [[02_Knowledge/Spring_Core/DI.md|DI]] 는 IoC 의 구현 방식 중 하나이다.
- [[02_Knowledge/Spring_Core/자동 구성.md|자동구성]] 은 IoC 컨테이너가 구성 클래스를 분석하여 Bean을 자동으로 주입하는 기능