### @Configuration과 바이트코드 조작의 마법
* 스프링 컨테이너는 싱글톤 레지스트리로 스프링 빈이 싱글톤이 되도록 보장해줘야 한다.
* 스프링이 자바 코드까지 어떻게 하기는 어렵다.
* 원래라면 앞서서 자바코드(memberRepository)가 3번 호출되어야 한다.

----

### 왜 그런지 알아보자
``` java

    @Test
    void configurationDeep(){
        ApplicationContext ac = new AnnotationConfigApplicationContext(AppConfig.class);
        AppConfig bean = ac.getBean(AppConfig.class);

        System.out.println("bean = " + bean.getClass());
    }
    
    결과값 -> bean = class hello.core.AppConfig$$EnhancerBySpringCGLIB$$75f7dade
    
```
* 순수한 클래스라면 class hello.core.AppConfig 까지만 출력되어야 한다.
* 하지만 예상과는 다르게 AppConfig 뒤에 xxxCGLIB 등이 붙게된다.
* 이 것은 내가 만든 클래스가 아니라 스프링이 CGUB라는 바이트 조작 라이브러리를 사용해서 AppConfig 클래스를 상속받은 임의의 다른 클래스 생성
* 그 다른 클래스를 스프링 빈으로 등록한 것이다.


