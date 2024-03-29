# Tech Interview - Spring

> 서블릿이 뭔가요?

**서블릿**이란 HTTP 클라이언트 요청과 응답에 대한 표준을 정의한 자바 클래스입니다.
서블릿은 HTTP 요청을 처리하고, 클라이언트에게 응답을 보내는 역할을 합니다.
이를 통해 웹 서버에서 동적인 페이지를 생성하고, 클라이언트에게 전달할 수 있습니다.
서블릿은 톰캣과 같은 서블릿 컨테이너에서 실행됩니다.

> 서블릿 컨테이너가 무엇인가요?

**서블릿 컨테이너**는 서블릿 인스턴스를 생성, 초기화, 소멸 등 생명주기를 관리하며, 
클라이언트 요청을 서블릿에게 전달하고, 서블릿의 응답을 클라이언트에게 전달하는 역할을 합니다.
이때 서블릿 인스턴스는 싱글톤으로 관리되며, 요청이 들어올 때마다 새로운 쓰레드를 생성하여 요청을 처리합니다.
대표적인 예시로 **톰캣**이 있습니다.

> 서블릿의 동작 방식에 대해 설명해주세요.

톰캣과 같은 서블릿 컨테이너는 클라이언트에서 요청이 오면
해당 요청을 처리할 서블릿을 찾아서 요청을 전달합니다.

요청에 해당하는 서블릿이 처음 호출될 때, 서블릿 컨테이너는 서블릿 인스턴스를 생성하고, 초기화합니다.
생성된 서블릿 인스턴스는 싱글톤으로 관리되며, 이후 요청이 들어올 때마다 새로운 쓰레드를 생성하여 요청을 처리합니다.

서블릿은 요청을 처리하고, 응답을 생성하여 서블릿 컨테이너에 전달합니다.
서블릿 컨테이너는 생성된 응답을 클라이언트에게 전달합니다.

> 스프링이 뭔지 간단히 설명해보세요

**스프링 프레임워크**는 자바 엔터프라이즈 애플리케이션을 개발하기 위한 오픈 소스 프레임워크입니다.
스프링은 내부에서 컨테이너를 통해 자바 객체의 **생명주기를 관리**하며,
의존관계 주입(DI)을 통해 **객체지향 설계**를 할 수 있도록 도와줍니다.
또한, 스프링은 AOP(Aspect Oriented Programming)를 지원하여,
트랜잭션, 보안, 로깅 등의 **관심사를 분리**하여 모듈화할 수 있습니다.

> 스프링 프레임워크는 왜 쓰나? 스프링의 특징에 대해 아는대로 이야기 해봐라

스프링의 특징으로는 IoC/DI, AOP, PSA가 있습니다.

먼저 IoC/DI는 제어의 역전과 의존성 주입을 의미합니다.
스프링에서는 `DI 컨테이너`를 사용하여, 객체 간의 의존관계를 외부에서 주입받아 사용할 수 있게 되어있습니다.
이를 통해 구현 클래스가 아니라 인터페이스에 의존하도록 하여, 객체 지향적으로 코드를 작성하고, 유연성을 높일 수 있습니다.

AOP는 관점 지향 프로그래밍을 의미하고, 횡단 관심사를 분리하여 비니스로직에 집중할 수 있도록 하는 기능입니다.
`AOP`를 사용하면, 트랜잭션, 보안, 로깅 등의 공통된 관심사를 분리하여 모듈화할 수 있고,
이를 통해 핵심 비즈니스 로직과 횡단 관심사를 분리하여 코드의 가독성과 유지보수성을 높일 수 있습니다.

PSA는 Portable Service Abstraction의 약자로, 서비스 추상화를 의미합니다.
스프링은 다양한 기술에 대한 추상화된 인터페이스르 제공하기 때문에
이를 통해 개발자는 특정 기술에 종속되지 않고, 다양한 기술을 사용할 수 있습니다.
ApplicationContext, TransactionManager, Micrometer, Slf4j 등이 PSA의 예시입니다.


> 스프링 프레임워크는 요청을 어떻게 처리하는지 전반적인 흐름을 설명해봐라

스프링에서 클라이언트의 요청을 받으면,
먼저 Filter를 거쳐서 DispatcherServlet으로 요청이 전달됩니다.
DispatcherServlet은 HandlerMapping 을 통해 요청을 처리할 컨트롤러를 찾고,
HandlerInterceptor를 거쳐서 HandlerAdapter를 통해 컨트롤러를 실행합니다.
컨트롤러에서는 비즈니스 로직을 처리하고, 처리 결과를 Model에 저장합니다.
DispatcherServlet에 반환하기 전에 다시 HandlerInterceptor를 거치고,
DispatcherServlet은 ViewResolver를 통해 응답을 보낼 View를 찾습니다.
마지막으로 다시 Filter를 거쳐서  View를 클라이언트에게 전달합니다.

```mermaid
graph LR
    Client -- Request --> Filter --> DispatcherServlet  -- Response --> Client
    
    DispatcherServlet <--> HandlerMapping
    
    DispatcherServlet --> HandlerInterceptor --> HandlerAdapter --> Controller\nService\nRepository --> HandlerInterceptor --> DispatcherServlet
    
    DispatcherServlet --> ViewResolver -- View --> DispatcherServlet
```
> 스프링이랑 스프링 부트는 차이점이 뭔가요?

**스프링**이란 스프링 프레임워크 뿐만 아니라 스프링 프로젝트 전반을 의미하는 것으로 알고 있습니다.
그 중에 가장 핵심 기술을 제공하는 스프링 프레임워크를 보통 스프링이라고 줄여서 부르는데,
스프링 프레임워크를 사용하여 개발할 때 다양한 스프링 프로젝트와
외부 라이브러리를 사용할 일이 많아지면서 스프링 부트가 등장한 것으로 알고 있습니다.

**스프링 부트**는 스프링 프레임워크를 사용하여 개발할 때,
설정을 간소화하고, 빠르게 개발할 수 있도록 도와주는 도구라고 알고 있습니다.
스프링 부트는 내장형 톰캣을 사용하여 별도의 서버 설정 없이도 웹 애플리케이션을 실행할 수 있고,
스프링 프레임워크에서 설정해야 했던 많은 설정들을 자동으로 설정해주는 것으로 알고있습니다.

> 스프링 컨테이너란?

**스프링 컨테이너**는 **빈(Bean)의 생명주기를 관리**하고, **의존성을 주입**하는 역할을 합니다.
스프링 컨테이너는 빈 팩토리(BeanFactory)와 애플리케이션 컨텍스트(ApplicationContext)로 구분됩니다.

**빈 팩토리**는 빈을 생성하고, 의존성을 주입하는 기능을 기본적인 제공하며,
**애플리케이션 컨텍스트**는 빈 팩토리의 하위 인터페이스로서, 빈 팩토리가 지원하지 않는 메시지 소스, 국제화 등 추가적인 기능들을 제공합니다.
 - 메시지 소스 : messages.properties 파일을 읽어서 메시지 관리
 - 국제화 : Locale에 따라 다른 messages.properties를 읽어서 메시지 관리

> IoC/DI가 무엇인가요?

IoC(Inversion of Control)란 제어의 역전을 의미하며,
객체의 생성과 생명주기의 관리를 프레임워크가 담당하는 것을 의미합니다.
DI(Dependency Injection)는 IoC의 구현 방법 중 하나로,
객체 간의 의존관계를 외부에서 주입받아 사용하는 것을 의미합니다.

IoC/DI를 사용하면, 객체 간의 의존관계를 외부에서 주입받아 사용할 수 있으며,
이를 통해 객체 간의 결합도를 낮추고, 유연한 코드를 작성할 수 있습니다.
유연하고 변경이 용이하다는 것은 새로운 기능을 추가하거나, 기존의 기능을 변경할 때,
**기존의 코드를 수정하지 않고**, 새로운 코드를 추가하거나 변경할 수 있다는 것을 의미합니다.

> 의존성 주입이 무엇인지? 왜 쓰는지 설명해달라

**의존성 주입(DI)**이란 객체 간의 의존관계를 외부에서 주입받아 사용하는 것을 의미합니다.
의존성 주입을 사용하면, 객체 간의 결합도를 낮춰 객체 지향적으로 코드를 작성할 수 있습니다.
객체 지향적인 코드는 유연하고 변경이 용이하다는 것을 의미합니다.
또한 유연하고 변경이 용이하다는 것은 새로운 기능을 추가하거나, 기존의 기능을 변경할 때,
**기존의 코드를 수정하지 않고**, 새로운 코드를 추가하거나 변경할 수 있다는 것을 의미합니다.

의존성 주입 없이 다른 클래스의 인스턴스를 사용하기 위해서는 해당 클래스의 인스턴스를 직접 생성해야합니다.
만약 해당 클래스가 변경 또는 삭제되면, 해당 클래스를 사용하는 모든 클래스를 수정해야합니다.

하지만 의존성 주입을 사용하면, 해당 클래스를 사용하는 클래스는
해당 클래스의 인스턴스를 외부에서 주입받아 사용하기 때문에,
해당 클래스가 변경 또는 삭제되어도, 해당 클래스를 사용하는 클래스를 수정할 필요가 없습니다.

> Spring에서 DI를 구현하는 자바 기술은 뭔가요?

Spring에서 DI를 구현하기 위해서 `Annotation`, `XML`, `자바 Config 클래스`를 사용할 수 있습니다.

Annotation 기반 DI는 @Component와 @Autowired와 같은 어노테이션을 사용하여 의존성을 주입할 수 있습니다.
빈 인스턴스로 등록할 클래스에 @Component을 붙이고, 의존성을 주입받을 필드에 @Autowired를 붙이면,
스프링 컨테이너가 해당 클래스의 인스턴스를 생성하고, 의존성을 주입해줍니다.

XML 기반 DI는 XML 파일에 빈 설정을 작성하여 의존성을 주입할 수 있습니다.
XML 파일에 빈 설정을 작성하고, 빈 설정을 읽어서 빈 인스턴스를 생성하고, 의존성을 주입해줍니다.

자바 설정 클래스를 사용하면, 자바 클래스에 @Configuration을 붙여서 빈 설정을 작성할 수 있습니다.
빈 설정 클래스에 @Bean을 붙여서 빈 인스턴스를 생성하고, 의존성을 주입해줍니다.

> Spring DI/IOC는 무엇이고, 어떻게 동작하는가?

DI/IOC는 스프링에서 객체 간의 의존관계를 외부에서 주입받아 사용하는 것을 의미합니다.
스프링에서 DI/IOC를 사용하면, 객체 간의 결합도를 낮추고, 유연한 코드를 작성할 수 있습니다.

스프링에서 빈 팩토리(BeanFactory) 혹은 애플리케이션 컨텍스트(ApplicationContext)라는 컨테이너를 사용하여
객체의 생명주기를 관리하고, 의존성을 주입합니다.

컨테이너에서 빈 객체를 생성하고 의존성을 주입하는 과정은 다음과 같습니다.
1. 빈 설정을 읽어서 빈 객체를 생성합니다.
2. 빈 객체의 의존성을 주입합니다.
3. 초기화 콜백 메서드를 통해 빈 객체를 초기화합니다. 
4. 초기화가 완료된 빈 객체는 컨테이너에 의해 관리되며, 컨테이너가 소멸될 때까지 유지됩니다.
5. 컨테이너가 되기 직전에 소멸 콜백 메서드가 호출되어 빈 객체를 소멸합니다.  

> AOP(Aspect Oriented Programming)가 무엇인가요?

AOP(Aspect Oriented Programming)란 **관점 지향 프로그래밍**을 의미합니다.
AOP는 **관심사를 분리**하여 모듈화하는 프로그래밍 기법으로,
트랜잭션, 보안, 로깅 등의 공통된 관심사를 분리하여 모듈화하는 것을 의미합니다.

AOP는 핵심 비즈니스 로직과 공통된 관심사를 분리하여 코드의 가독성과 유지보수성을 높일 수 있으며,
핵심 비즈니스 로직에 영향을 주지 않고 공통된 관심사를 추가하거나 제거할 수 있습니다.

> AOP 용어들을 설명해보세요.

* 어드바이스(Advice) : 부가 기능, 실제로 어떤 일을 하는지 정의한 코드를 의미합니다.
  * Around, Before, After 등 다양한 종류가 있습니다.
* 조인 포인트(Join Point) : 어드바이스를 적용할 수 있는 위치, 메서드 호출, 필드 접근 등이 조인 포인트가 될 수 있습니다.
  * 스프링 AOP에서는 메서드 호출만 조인 포인트로 지정할 수 있습니다.
* 포인트 컷(Pointcut) : 조인 포인트 중에서 어드바이스가 적용될 위치
  * AspectJ 표현식을 사용하여 메서드를 지정합니다.
* 타겟(Target) : 실제로 어드바이스가 적용되는 대상
* 애스팩트(Aspect) : 여러 어드바이스와 포인트 컷을 모듈화한 것, 
  * 여러 개의 어드바이스와 포인트 컷을 하나의 애스팩트로 묶어서 사용합니다.
  * @Asepct를 사용하여 정의합니다.
* 어드바이저(Advisor) : 하나의 포인트 컷과 하나의 어드바이스를 결합한 것
* 위빙(Weaving) : 어드바이스를 타겟의 조인 포인트에 적용하는 과정
  * 컴파일 시점, 클래스 로딩 시점, 런타임 시점에 적용할 수 있지만,
  * 스프링 AOP에서는 프록시 패턴을 사용하기 때문에 런타임 시점에만 적용합니다.
* AOP 프록시: AOP 기능을 구현하기 위한 프록시 객체
  * 스프링에서는 JDK 동적 프록시와 CGLIB 프록시를 사용하여 AOP를 구현합니다.

> MVC 패턴이란?

MVC 패턴이란 Model, View, Controller의 약자로,
비즈니스 로직과 사용자 인터페이스를 분리하여 개발하는 디자인 패턴입니다.

* Model : 뷰에 출력할 데이터를 담아두는 부분
* View : 사용자에게 보여지는 화면을 담당하는 부분
* Controller : 사용자의 입력을 받아 비즈니스 로직을 실행하는 부분

MVC패턴을 사용하면 사용자 인터페이스와 비즈니스 로직을 분리해서 
서로 영향을 끼치지 않고 개발할 수 있으며, 유지보수성이 높은 코드를 작성할 수 있습니다.

> MVC1이랑 MVC2 패턴 차이에 대해 설명해주세요.

**MVC1**은 JSP와 같이 프레젠테이션 로직과 비즈니스 로직이 함께 작성되어 있는 방식입니다.
JSP에서는 비즈니스 로직과 프레젠테이션 로직이 함께 작성되어 있어, 유지보수성이 떨어지는 단점이 있습니다.

반면, **MVC2**에서는 프레젠테이션 로직과 비즈니스 로직을 분리하여 개발하는 방식입니다.
비즈니스 로직을 servlet으로 분리시켜서 비즈니스 로직과 프레젠테이션 로직이 서로 영향을 끼치지 않도록 개발할 수 있습니다.

**스프링**은 DispatcherServlet을 통해 클라이언트의 요청을 받아서 Controller로 전달하고,
컨트롤러에서 비즈니스 로직을 처리한 후, 결과를 Model에 담아서 View로 전달하는 방식으로 MVC2 패턴을 구현합니다.

> 스프링 MVC 구조 흐름에 대해 과정대로 설명해보세요.

1. 클라이언트의 요청은 Filter를 거쳐서 DispatcherServlet에 도착합니다.
2. DispatcherServlet은 HandlerMapping을 통해 요청을 처리할 컨트롤러를 찾습니다.
3. HandlerInterceptor를 거쳐서 HandlerAdapter를 통해 컨트롤러를 실행합니다.
4. 컨트롤러에서 비즈니스 로직을 처리하고, 처리 결과를 Model에 저장합니다.
5. DispatcherServlet에 반환하기 전에 다시 HandlerInterceptor를 거치고,
6. DispatcherServlet은 ViewResolver를 통해 응답을 보낼 View를 찾고,
7. 다시 Filter를 거쳐서 해당 View를 클라이언트에게 전달합니다.

> DispatcherServlet이 무엇인가요?

DispatcherServlet이란 클라이언트의 요청을 처리할 수 있는
컨트롤러에 위임하는 **Front Controller**라고 할 수 있습니다.

DispatcherServlet은 클라이언트의 요청을 받아서,
HandlerMapping을 통해 요청을 처리할 컨트롤러를 찾고,
HandlerAdapter를 통해 해당 컨트롤러를 실행합니다.

> 어떻게 하나의 컨트롤러로 여러 요청을 받을 수 있을까요?

톰캣과 같은 서블릿 컨테이너는 클라이언트의 요청이 들어오면,
**새로운 스레드를 생성**하여 해당 요청을 처리하기 때문에 
하나의 컨트롤러 인스턴스를 사용하여 여러 요청을 동시에 처리할 수 있습니다.

또한 스프링 MVC에서는 `@RequestMapping`을 사용하여 하나의 컨트롤러로 여러 요청을 받을 수 있습니다.
`@RequestMapping`의 **method** 옵션 사용하여 Http Method에 따라 요청을 분기할 수 있으며,
**value** 옵션을 사용하여 요청 URL에 따라 요청을 분기할 수 있습니다.

> Filter와 Interceptor의 차이가 무엇인가요?

스프링에서 Filter와 Interceptor는 모두 클라이언트의 요청을 중간에 가로채어
인증/인가, 인코딩/디코딩 등 공통의 관심사를 분리하여 처리는 기능을 제공합니다.

Filter는 서블릿 컨테이너에서 제공하는 기능으로, 클라이언트의 요청을 받기 전후로 호출됩니다.
서블릿 컨테이너 내부에서 동작하므로, 모든 요청과 서블릿에 대해 적용됩니다.
또한 Filter는 체인으로 구성되어 있어서 FilterChain을 통해 다음 필터로 요청을 전달할 수 있고,
chain.doFilter()에 다른 요청을 전달할 수도 있습니다.
하지만 서블릿에서 제공하는 기능이기 때문에 ExceptionHandler를 통해 예외처리가 되지 않으므로,
예외가 발생하면 서블릿 컨테이너까지 예외가 전달됩니다.
* doFilter()

Interceptor는 스프링에서 제공하는 기능으로, DispatcherServlet에서 HandlerAdapter가 호출되기 전에 호출됩니다.
Interceptor도 Filter와 마찬가지로 체인으로 구성되어 있습니다.
하지만 Filter와는 달리, 단계가 세분화 되어있고 더 많은 기능을 제공합니다.
스프링 내부에서 동작하기 때문에 스프링의 빈과 컨텍스트에 접근할 수 있고,
예외가 발생했을 때 ExceptionHandler를 통해 예외를 처리할 수 있습니다.
* preHandle(), postHandle(), afterCompletion()

> Spring Bean(빈)이란?

스프링에서 빈이란 스프링 컨테이너에 의해 관리되는 객체를 의미합니다.
빈 인스턴스는 스프링 컨테이너에 의해 생성, 초기화, 소멸됩니다.

> POJO란 무엇인가요?

POJO(Plain Old Java Object)란 순수한 자바 객체를 의미합니다.
과거 EJB(Enterprise JavaBeans)와 같은 기술들이 복잡한 인터페이스와 상속을 요구했던 반면,
스프링은 POJO를 사용하여 간단하고 직관적인 코드를 작성할 수 있도록 도와줍니다.

> 스프링에서 빈(Bean)을 등록하는 방법에 대해 말해보세요.

빈을 등록하는 방법은 크게 3가지가 있습니다.
1. XML 파일에 빈 설정을 작성하는 방법
   * `<bean>` 태그에 id와 classpath를 설정하여 빈을 등록합니다.
2. Annotation을 사용하여 빈을 등록하는 방법
   * `@Component`, `@Service`, `@Repository`, `@Controller` 등의 어노테이션을 사용하여 빈을 등록합니다.
3. 자바 설정 클래스를 사용하여 빈을 등록하는 방법
   * `@Configuration`을 사용하여 빈 설정 클래스를 정의하고, `@Bean`을 사용하여 빈을 등록합니다.

> 스프링 빈의 라이프사이클은 어떻게 관리되는지 설명해주세요.

```mermaid
graph LR
  1["스프링 컨테이너 생성"] --> 2["빈 인스턴스 생성"] --> 3["의존성 주입"] --> 4["초기화 콜백"] --> 5["빈 사용"] --> 6["소멸 콜백"] --> 7["스프링 컨테이너 소멸"]
```
* 생성자 주입은 빈 인스턴스 생성 시 의존성을 주입합니다.

> Spirng Bean의 Scope에 대해 설명하시오.

빈 스코프란 빈이 존재할 수 있는 범위를 의미합니다.
스프링에서 제공하는 대표적인 빈 스코프는 싱글톤, 프로토타입이 있습니다.
* 싱글톤(Singleton)
  * 하나의 빈 인스턴스를 생성하여 모든 요청에 대해 같은 인스턴스를 반환합니다.
  * 기본 스코프로, 스프링 컨테이너가 생성될 때부터 소멸될 때까지 유지됩니다.
* 프로토타입(Prototype)
  * 컨테이너에 빈 요청이 들어올 때마다 새로운 빈 인스턴스를 생성하여 반환합니다. 
  * 빈의 생성과 의존관계 주입, 초기화 콜백까지만 관여하고 더 이상 관리하지 않습니다.

웹 스코프는 웹 환경에서만 동작하는 스코프로, Request, Session, Application, WebSocket 스코프가 있습니다.
* 리퀘스트(Request) : HTTP 요청마다 새로운 빈 인스턴스를 생성하여 반환합니다.
* 세션(Session) : HTTP 세션마다 새로운 빈 인스턴스를 생성하여 반환합니다.
* 어플리케이션(Application) : 웹 어플리케이션마다 새로운 빈 인스턴스를 생성하여 반환합니다.
* 웹소켓(WebSocket) : 웹소켓 연결마다 새로운 빈 인스턴스를 생성하여 반환합니다.

> Spring의 싱글톤 패턴에 대해 설명해주세요.

싱글톤 패턴이란 하나의 클래스로부터 단 하나의 인스턴스만을 생성하여 사용하는 디자인 패턴을 의미합니다.
스프링에서 빈 인스턴스는 기본적으로 싱글톤 패턴을 따르며, 스프링 컨테이너가 생성될 때부터 소멸될 때까지 유지됩니다.
스코프 어노테이션 통해서 싱글톤이 아닌 다른 스코프로 변경할 수 있습니다.

> Spring의 스코프 프로토 타입 빈에 대해 설명해주세요.

프로토 타입 빈 스코프는 빈이 생성될 때마다 새로운 인스턴스를 생성하여 반환합니다.
프로토타입 빈은 스프링 컨테이너가 생성과 의존성 주입, 초기화 콜백까지만 관여하고, 더 이상 관리하지 않습니다.

프로토 타입 빈은 컨테이너에 요청될 때에 새로운 인스턴스를 생성하는 것이기 때문에
싱글톤 빈에서 프로토 타입 빈을 주입받아 사용하면 해당 참조값을 유지하게 되고,
서로 다른 클라이언트가 같은 프로토타입 빈을 사용하게되는 문제가 발생할 수 있습니다.

스프링에서는 빈 스코프로 인해 발생하는 문제를 해결하기 위해 `ObjectProvider`를 제공합니다.
`ObjectProvider`은 직접 의존관계를 조회하는 DL(Dependency Lookup)을 지원하는 인터페이스입니다. 
`ObjectProvider`를 사용하면 프로토타입 빈을 사용할 때마다 새로운 인스턴스를 생성하여 반환합니다.
* 추가로 DL은 지연 참조를 해야하거나 순환 참조 문제가 발생할 때 사용할 수 있습니다.

> Spring에서 서비스와 컴포넌트의 차이

`@Component`는 스프링 빈으로 등록하는 어노테이션입니다.
스프링 컨테이너(ApplicationContext)는 해당 어노테이션이 붙은 클래스를 스캔하여 빈으로 등록합니다.
* 컴포넌트 자동주입하기 위해서는 설정 클래스에 @ComponentScan 어노테이션을 붙여야합니다.
* @ComponentScan을 붙이면 basePackages에 지정된 패키지부터 하위 패키지까지 스캔하여 @Component 어노테이션이 붙은 클래스를 빈으로 등록합니다.
* 또한 @Component을 사용해서 의존관계를 주입하기 위해서는 @Autowired 어노테이션을 사용하거나 생성자 주입을 사용합니다.

`@Service`는 `@Component`를 상속받은 어노테이션으로, 
레이어드 아키텍처에서 비즈니스 로직을 담당하는 클래스에 붙입니다.

> Controller, RestController는 뭐가 다른가요? 응답이 어떻게 다른가요?

Controller는 동적으로 HTML 페이지를 생성하는데 사용되는 어노테이션입니다.
Controller 클래스는 View 레이어와 상호작용하고, 사용자가 브라우저를 통해 요청한 페이지를 반환합니다.
Controller 메서드는 주로 ModelAndView 객체를 반환하며, View 이름과 Model을 함께 반환합니다.
* 메서드에 @ResponseBody를 사용하면, @RestController와 같이 HTTP Response Body에 데이터를 담아 반환할 수 있습니다. 

RestController는 RESTful 웹서비스를 위해 JSON, XML 등의 데이터를 반환하는데 사용되는 어노테이션입니다.
RestController는 View 레이어와 상호작용하지 않고, 사용자가 브라우저를 통해 요청한 데이터를 HTTP Response Body에 반환합니다.
RestController에서 메서드를 통해 객체를 반환하면 JSON 형태로 변환되어 HTTP Response Body에 담겨서 반환됩니다.
* @Controller + @ResponseBody와 같은 역할을 합니다.

> Spring MVC 에서 요청이 들어왔을 때부터 응답이 나갈 때까지의 흐름을 설명해주세요.

1. 클라이언트의 요청은 Filter를 거쳐서 DispatcherServlet에 도착합니다.
2. DispatcherServlet은 HandlerMapping을 통해 요청을 처리할 컨트롤러를 찾습니다.
3. HandlerInterceptor를 거쳐서 HandlerAdapter를 통해 컨트롤러를 실행합니다.
4. 컨트롤러에서 비즈니스 로직을 처리하고, 처리 결과를 Model에 저장합니다.
   * @RestController를 사용하면, 해당 객체를 반환합니다.
5. DispatcherServlet에 반환하기 전에 다시 HandlerInterceptor를 거치고,
6. DispatcherServlet은 ViewResolver를 통해 응답을 보낼 View를 찾고,
   * @RestController를 사용하면, HttpMessageConverter를 사용하여 객체를 JSON 형태로 변환하여 반환합니다.
7. 다시 Filter를 거쳐서 해당 View를 클라이언트에게 전달합니다.

> @RequestBody, @RequestParam, @ModelAttribute의 차이를 설명해주세요.

`@RequestParam`은 단순하게 HTTP 요청 파라미터를 매개변수로 받아오는 어노테이션입니다.

`@RequestBody`는 HTTP 요청의 body에 담긴 데이터를 자바 객체의 필드에 바인딩해서 받아오는 어노테이션이고,

`@ModelAttribute`는 HTTP 요청 파라미터를 자바 객체로의 필드에 바인딩해서 받아오는 어노테이션 입니다.

> HttpMessageConverter란 무엇인가요?

HttpMessageConverter는 @ResponseBody, @RequestBody 어노테이션을 사용하여
HTTP 요청과 응답의 body에 담긴 데이터를 객체로 변환하거나, 객체를 특정 데이터 형식으로 변환하는 역할을 합니다.

스프링에서는 다양한 HttpMessageConverter를 제공하며,
요청의 Content-Type과 응답의 Accept 헤더에 따라 적절한 HttpMessageConverter를 선택하여 사용합니다.

응답의 경우에는 컨트롤러의 메서드에 @ResponseBody 어노테이션을 사용하거나,
클래스를 @RestController 어노테이션을 사용하면 객체를 HTTP 응답의 body에 담아 반환할 수 있습니다.
* XML 형식으로 반환하기 위해서는 MappingJackson2XmlHttpMessageConverter를 빈 인스턴스로 등록하고
* `produces` 옵션의 값을 `MediaType.APPLICATION_XML_VALUE`로 설정하면 됩니다.

> ViewResolver란 무엇인가요?

ViewResolver란 컨트롤러에서 반환한 View 이름을 통해 실제 View 객체를 찾아주는 역할을 합니다.

SpringMVC에서는 정적 리소스를 반환하거나,
JSP, Thyemleaf와 같은 템플릿 엔진에 Model을 전달하여 동적으로 HTML을 생성하여 반환할 수 있습니다.

> ExceptionResolver란 무엇인가요?

스프링에서 예외가 발생했을 때 DispatcherServlet는 **ExceptionResolver**를 통해 예외를 처리합니다.
스프링에서 제공하는 **ExceptionResolver**는 다음과 같습니다.
* ExceptionHandlerExceptionResolver (*중요)
  * `@ExceptionHandler` 어노테이션을 사용하여 컨트롤러 내부에서 예외를 처리할 수 있습니다.
  * 컨트롤러 내부에서 예외처리 메서드를 작성하고
    `@ExceptionHandler` 어노테이션에 처리할 예외 클래스를 지정하면 됩니다.
    추가로 `@ResponseStatus`를 지정하면 응답 상태 코드를 지정할 수 있습니다.
* ResponseStatusExceptionResolver
  * `@ResponseStatus` 어노테이션가 붙은 예외 클래스에 대한 예외 처리를 자동으로 처리합니다.
* DefaultHandlerExceptionResolver
  * 스프링에서 미리 정의한 예외(`TypeMismatchException` 등)들에 대한 처리를 담당합니다.

추가로 예외가 발생하면 postHandle은 호출되지 않지만, afterCompletion은 호출됩니다.

```mermaid
graph LR
  WAS -- Request --> Dispatcher\nServlet
  Dispatcher\nServlet -- Response --> WAS

  Dispatcher\nServlet -- 1 --> preHandle
  Dispatcher\nServlet -- 2 --> HandlerAdapter --> 1["Controller\n(예외발생)"]
  Dispatcher\nServlet -- X --> postHandle
  Dispatcher\nServlet -- 3 --> ExceptionResolver
  Dispatcher\nServlet -- 4 --> afterCompletion
  Dispatcher\nServlet -- 5 --> ViewResolver
```

> ControllerAdvice가 무엇인가요?

ControllerAdvice는 **전역 예외 처리**를 위한 어노테이션입니다.
`@ControllerAdvice`를 사용하여 예외 처리 클래스를 정의하고, `@ExceptionHandler`를 사용하여 예외 처리 메서드를 정의하면,
해당 클래스에서 정의한 예외를 전역적으로 처리하거나, 특정 컨트롤러를 지정하여 예외를 처리할 수 있습니다.

> Field 주입과 생성자 주입, Setter 주입

스프링에서 의존성 주입을 하는 방법은 크게 3가지가 있습니다.
1. Field 주입
   * 필드에 `@Autowired` 어노테이션을 사용하여 의존성을 주입합니다.
   * 코드가 간결하고 직관적이지만, DI 프레임워크 없이는 테스트할 수 없다는 단점이 있습니다.
   * 또한 객체의 불변성을 보장할 수 없다는 단점이 있습니다.
2. 생성자 주입
   * 생성자에 `@Autowired` 어노테이션을 사용하여 의존성을 주입합니다.
   * 생성자 주입을 사용하면, 객체를 생성하는 시점에 의존성을 주입받기 때문에, 객체의 불변성을 보장할 수 있습니다.
   * 또한 테스트시 DI 프레임워크가 없어도 객체를 생성하여 테스트할 수 있습니다. 
3. Setter 주입
   * Setter 메서드에 `@Autowired` 어노테이션을 사용하여 의존성을 주입합니다.
   * Setter 주입은 객체 생성 후에 의존성을 주입받기 때문에, DI 프레임워크가 없어도 객체를 생성하여 테스트할 수 있지만,
   * 객체의 불변성을 보장할 수 없다는 단점이 있습니다.

> WebFlux 써보셨나요?

WebFlux를 사용해 본 적은 없지만, Javascript와 같이 이벤트 루프 기반의 비동기 프로그래밍을 지원하는 프레임워크로 알고 있습니다.
기존의 Spring MVC는 스레드 풀을 생성하여 요청을 처리하는 반면,
WebFlux는 Non-blocking 방식으로 요청을 처리하는 것으로 알고 있습니다.
또한 Project Reactor 라이브러리를 사용하여 리액티브 프로그래밍을 지원하는 것으로 알고 있습니다.
* project reactor는 발행-구독 모델 기반의 reactive streams를 구현한 라이브러리입니다. 

> Reactive Programming이 무엇인가요?
