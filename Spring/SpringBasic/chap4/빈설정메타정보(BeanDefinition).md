### 스프링 빈 설정 메타정보
#### BeanDefinition
* 스프링은 어떻게 다양한 설정 형식을 지원하는 걸까?
  * 그 중심에는 BeanDefinition이라는 추상화가 있기 때문이다.
  * 쉽게 역할과 구현을 개념적으로 나눈 것이다.
  * 스프링 입장에서는 XML인지 JAVA인지 알필요없이 BeanDefinition만 알면 된다.
  * BeanDefinition을 빈 설정 메타정보라고 한다.
  * 스프링 컨테이너는 이 메타정보를 기반으로 스프링 빈을 생성한다.

```

    스프링 컨테이너 --> BeanDefinition
                          |
                          |
             --------------------------------
             |             |                |
       AppConfig.class   appConfig.xml    appConfig.xxx

```

