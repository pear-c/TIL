---
aliases:
  - "\bDI"
---
# DI (Dependency Injection)

## 🔍 정의

### 의존성 주입
: 의존 객체를 직접 생성하지 않고 외부에서 주입받는 방식

Spring 에서는 [[02_Knowledge/Spring_Core/자동 구성.md|객체를 Bean 으로 등록]]하여 컨테이너가 관리한다.

**Bean 으로 등록한 객체들이 필요로 하는 의존성을 개발자가 아니라, 외부에서 직접 주입받는 것을 DI 라고 한다.**

DI 라고 해서 특별한건 아니고, 앞서 설명한 IoC 의 패턴 중 하나일 뿐이다. 그리고 스프링에서는 **@Autowired** 라는 어노테이션을 이용해 객체 간의 의존성을 주입해준다.

---
## 📂 종류

- 생성자 주입 (추천)
- setter 주입
- 필드 주입 (비추천)

---
## 🔧 예시

## 1. 생성자 주입 (Constructor Injection)

```java
@Component 
public class AppStartupRunner implements ApplicationRunner { 
	private HighSchoolStudent highSchoolStudent; 
	private UniversityStudent universityStudent; 
	
	// @AutoWired (생략 가능) 
	public AppStartupRunner(HighSchoolStudent highSchoolStudent, UniversityStudent universityStudent) { 
	this.highSchoolStudent = highSchoolStudent; 
	this.universityStudent = universityStudent; 
	} 
}
```

주입 받을 객체를 선언한다. 그리고 생성자를 생성하여 해당 객체에 의존성을 주입하면 된다. (이때, 롬복도 사용 가능하다.)

> [!Lombok 생성자]
    > - @NoArgsConstructor : 인자를 포함하지 않는 생성자 자동 생성
    > - @AllArgsConstructor : 모든 인자 포함하는 생성자 자동 생성
    > - @RequiredArgsConstructor : 필요한 인자만 자동 생성 (private final)

이때, **생성자가 하나일 경우 @Autowired 생략이 가능하다.**

## 2. Setter 주입

```java
@Component 
public class AppStartupRunner implements ApplicationRunner { 

	private Greeting greeting; 
	
	@Autowired 
	public void setGreeting(Greeting greeting) { 
		this.greeting = greeting; 
	} 
	
	@Override 
	public void run(ApplicationArguments args) { 
		greeting.sayHello(); 
	} 
}
```

주입 받고 싶은 객체를 선언하고, Setter 를 이용해 의존성을 주입한다.

## 3. 필드 주입

```java
@Component 
public class AppStartupRunner implements ApplicationRunner { 
	@Autowired 
	private Greeting greeting; 
	
	@Override 
	public void run(ApplicationArguments args) { 
		greeting.sayHello(); 
	} 
}
```

---
## ✅ 장점

- 객체 간 결합도 ↓
- 테스트 용이성 ↑

---
## 🔗 관련

- [[IoC]] : DI는 IoC를 구현하는 수단
- [[자동 구성]] : DI 대상 객체를 자동으로 주입할 수 있음
- [[외부 구성]]



