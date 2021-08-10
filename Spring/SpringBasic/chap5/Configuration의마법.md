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

> 바로 이 임의로 만든 클래스가 싱글톤을 보장되도록 해주는 것이다.

----
### AppConfig@CGLIB의 예상코드

``` java

@Bean
public MemberRepository memberRepository(){

    if (memoryMemberRepository가 이미 스프링 컨테이너로 등록되어 있으면?){
        // Override가 되면서..
        return 스프링 컨테이너에서 찾아서 변환;
    }else { // 스프링 컨테이너에 없으면
         기존 로직을 호출해서 MemoryMemberRepository를 생성하고 스프링 컨테이너에 등록
         return 반환
        }
    } 

```

> @Bean이 붙은 메서드 마다 스프링 빈이 존재하면 존재하는 빈 반환, 없으면 스프링 빈으로 등록하고 반환하는 코드가 동적 생성 <br>
> 따라서 싱글톤이 보장되는 것이다.



