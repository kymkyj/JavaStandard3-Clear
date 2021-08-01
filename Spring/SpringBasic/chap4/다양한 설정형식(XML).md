### 다양한 설정 형식 지원 - XML
* 스프링 컨테이너는 다양한 형식의 설정형식을 받을 수 있게 유연하게 설계되어있다.
* 자바코드, XML 코드등이 대표적

```
                      BeanFactory
                      <<Interface>>
                            |
                            |
                    ApplicationContext
                      <<Interface>>
                            |
                --------------------------------------------
                |                 |                        |             
                |                 |                        |
           AnnotationConfig     GenericXml          ApplicationContext
           ApplicationContext   ApplicationContext         |    
                |                 |                        |
             AppConfig.class     appConfig.xml         appConfig.xxx

```

최근에는 주로 어노테이션 기반 자바코드 설정을 사용
* 지금까지 한것 처럼 new AnnotationConfigApplicationContext(AppConfig.class)
* AnnotationConfigApplicationContext 클래스를 사용하면서 자바 코드로 설정정보를 넘기면된다.

----

### XML 설정 사용
* XML 설정방식은 스프링 부트로 인해 잘 사용하지 않지만 레거시 프로젝트들은 이 방식을 사용한다.
* 컴파일 설정없이 빈 설정정보를 변경할 수 있음(xml파일 자체를 교체) 등의 장점이 있다.

### XML 설정 예시

``` xml

/* xml 방식은 네임 스페이스와 스키마속성을 갖는 <beans>안에 스프링빈설정 작성 */
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">

    <bean id="memberService" class="hello.core.member.MemberServiceImpl">
        <constructor-arg name="memberRepository" ref="memberRepository"/>
    </bean>

    <bean id="memberRepository" class="hello.core.member.MemoryMemberRepository"/>

    <bean id="orderService" class="hello.core.order.OrderServiceImpl">
        <constructor-arg name="memberRepository" ref="memberRepository"/>
        <constructor-arg name="discountPolicy" ref="discountPolicy"/>
    </bean>

    <bean id="discountPolicy" class="hello.core.discount.RateDiscountPolicy"/>
</beans>

```

* 형식만 xml 형태이지 자바코드로 된 설정파일(AppConfig.java)를 보면 거의 유사하다는 것을 알 수 있다.
* 다만, xml 방식은 최근에는 잘 사용하지 않는다.

