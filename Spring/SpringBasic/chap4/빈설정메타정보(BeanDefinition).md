### 스프링 빈 설정 메타정보
#### BeanDefinition
* 스프링은 어떻게 다양한 설정 형식을 지원하는 걸까?
  * 그 중심에는 BeanDefinition이라는 추상화가 있기 때문이다.
  * 쉽게 역할과 구현을 개념적으로 나눈 것이다.
  * 스프링 입장에서는 XML인지 JAVA인지 알필요없이 BeanDefinition만 알면 된다.
  * BeanDefinition을 빈 설정 메타정보라고 한다.
  * 스프링 컨테이너는 이 메타정보를 토대로 스프링 빈을 생성한다.

```

    스프링 컨테이너 --> BeanDefinition
                          |
                          |
             --------------------------------
             |             |                |
       AppConfig.class   appConfig.xml    appConfig.xxx

```

### BeanDefinition 살펴보기
* BeanClassName : 생성할 빈의 클래스 명(자바 설정처럼 팩토리 역할의 빈을 사용하면 없음)
* factoryBeanName : 팩토리 역할의 빈을 사용할 경우 이름 예) appConfig
* factoryMethodName : 빈을 생성할 팩토리 메서드 지정 예) memberService
* Scope : 싱글톤(기본값)
* lazyInit : 스프링 컨테이너를 생성할 때 빈을 생성하는 것이 아니라, 실제 빈을 사용할 때까지 최대한 생성을 지연처리 하는지 여부를 
* InitMethodName : 빈을 생성하고, 의존관계를 적용한 뒤에 호출되는 초기화 메서드명
* DestroyMethodName : 빈의 생명주기가 끝나서 제거하기 직전에 호출되는 메서드 명
* Constructor arguments, Properties : 의존관계 주입에서 사용한다.

