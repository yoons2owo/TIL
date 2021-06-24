# hello-spring

인프런 스프링 입문 - 코드로 배우는 스프링 부트, 웹 MVC, DB 접근 기술

강의 메모

[Repository](https://github.com/yoons2owo/hello-spring)

## 스프링 빈과 의존관계

### 컴포넌트 스캔과 자동 의존관계 설정

```java
@Controller
public class MemberController {

    private final MemberService memberService;

    @Autowired
    public MemberController(MemberService memberService) {
        this.memberService = memberService;
    }

}
```
- 스프링이 실행될 때 @Controller가 달린 객체를 생성해서 스프링 컨테이너에 넣어준다.
- @SpringBootApplication 내부의 @ComponentScan 애노테이션이 현재 패키지 하위의 @Component를 스캔해서 스프링 컨테이너의  스프링 빈으로 등록해준다.
- 스프링 컨테이너에서 스프링 빈이 관리된다고 표현한다.
- 생성자에 @Autowired가 있으면 객체 생성 시점에 스프링 컨테이너에서 해당 스프링 빈을 찾아서 주입한다.
- 이렇게 객체 의존관계를 외부에서 넣어주는 것을 DI(의존성 주입)라고 한다.
- 생성자가 1개만 있으면 @Autowired는 생략할 수 있다.


```
***************************
APPLICATION FAILED TO START
***************************

Description:

Parameter 0 of constructor in hello.hellospring.controller.MemberController required a bean of type 'hello.hellospring.service.MemberService' that could not be found.
```
- 이 상태로 스프링 애플리케이션을 실행하면 오류가 발생하는데, MemberService가 스프링 빈으로 등록되어 있지 않다는 것을 의미한다.

### 스프링 빈을 등록하는 2가지 방법
- 컴포넌트 스캔과 자동 의존관계 설정
- 자바 코드로 직접 스프링 빈 등록하기

#### 컴포넌트 스캔 원리
- @Component 애노테이션이 있으면 스프링 빈으로 자동 등록된다.
  ```java
  @Target(value=TYPE)
  @Retention(value=RUNTIME)
  @Documented
  @Indexed
  public @interface Component
  ```
- @Controller 가 있으면 스프링 빈으로 자동 등록된다.
- @Component 를 포함하는 다음 애노테이션도 스프링 빈으로 자동 등록된다.
  - @Controller
    ```java
    @Target({ElementType.TYPE})
    @Retention(RetentionPolicy.RUNTIME)
    @Documented
    @Component
    public @interface Controller
    ```
  - @Service
    ```java
    @Target({ElementType.TYPE})
    @Retention(RetentionPolicy.RUNTIME)
    @Documented
    @Component
    public @interface Service
    ```
  - @Repository
    ```java
    @Target(value=TYPE)
    @Retention(value=RUNTIME)
    @Documented
    @Component
    public @interface Repository
    ```
- 스프링은 스프링 컨테이너에 빈을 등록할 때, 기본으로 싱글톤으로 등록한다.(유일하게 하나만 등록해서 공유한다 = 같은 인스턴스를 공유한다) 따라서 같은 스프링 빈이면 모두 같은 인스턴스다. 설정으로 싱글톤이 아니게 설정할 수 있지만, 대부분 싱글톤을 사용한다.


#### 자바 코드로 직접 스프링 빈 등록하기
```java
@Configuration
public class SpringConfig {

    @Bean
    public MemberService memberService() {
        return new MemberService(memberRepository());
    }

    @Bean
    public MemberRepository memberRepository() {
        return new MemoryMemberRepository();
    }
}
```
- 향후 메모리 리포지토리를 다른 리포지토리로 변경할 예정이므로, 컴포넌트 스캔 방식 대신에
자바 코드로 스프링 빈을 설정한다.

### 참고
- DI 방법
  -  필드 주입: 의존관계를 바꿀 수 있는 방법이 없음 비권장
    ```java
    @Autowired
    private MemberService memberService;
    ```
  -  setter 주입: public하게 노출이 되므로 잘못 접근하면 문제
    ```java
    private MemberService memberService;

    @Autowired
    public void setMemberService(MemberService memberService) {
      this.memberService = memberService;
    }
    ```
  -  생성자 주입 : 의존관계가 실행중(런타임중)에 동적으로 변하는 경우는 거의 없으므로 조립되고 끝나는 생성자 주입을 권장
    ```java
    private MemberService memberService;

    @Autowired
    public MemberController(MemberService memberService) {
      this.memberService = memberService;
    }
    ```
- 실무에서는 주로 정형화된 컨트롤러, 서비스, 리포지토리 같은 코드는 컴포넌트 스캔을 사용한다. 
그리고 정형화 되지 않거나, 상황에 따라 구현 클래스를 변경해야 하면 설정을 통해 스프링 빈으로
등록한다.
- @Autowired를 통한 DI는 Controller, Service 등과 같이 스프링이 관리하는 객체에서만 동작한다. 스프링 빈으로 등록하지 않고 내가 직접 생성한 객체에서는 동작하지 않는다.

※ 스프링 빈이란?
- Spring IoC 컨테이너에 의해 관리되는 객체
- 인스턴스를 생성하고, 생명주기(life Cycle)를 수행하고, 의존성 주입(Dependency Injection) 한다는 것)
- Spring Bean은 IoC 컨테이너에서 관리되기 때문에, IoC 컨테이너에 등록을 해야 사용할 수 있게 된다.

※ 자바 빈이란?
- 데이터를 표현하는 것을 목적으로 하는 자바 클래스

- Java Bean 규약
  - 기본생성자가 존재해야한다.
  - 모든 멤버변수의 접근제어자는 private이다.
  - 멤버변수마다 getter/setter가 존재해야한다. (속성이 boolean일 경우 is를 붙힘)
  - 외부에서 멤버변수에 접근하기 위해서는 메소드로만 접근할 수 있다.
  - Serializable(직렬화)가 가능해야한다.(외부의 시스템에서도 사용할 수 있도록 변환. 예를 들어 Json이나 csv로 변환하는 것, Serializable interface를 implements한 클래스는 직렬화 할 수 있다.)