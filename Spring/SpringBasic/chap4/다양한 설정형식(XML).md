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


