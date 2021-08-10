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

----

### @Configuration이 없이 @Bean만 적용하면??
<img src= https://user-images.githubusercontent.com/32288986/128887518-695463a1-a0c0-4d50-99ad-c2e40b3a3080.png>

* 결과 값이 class hello.core.AppConfig 까지만 출력된다.
* 순수 자바코드가 돌면서 호출되는 만큼 memberRepository가 new로 생성되어 3번 출력되면서 싱글톤이 깨진다.

``` 
    memberService -> memberRepository = hello.core.member.MemoryMemberRepository@3fed2870
    orderService -> memberRepository = hello.core.member.MemoryMemberRepository@77128536
    memberRepository = hello.core.member.MemoryMemberRepository@58326051
    
    --> 각각 다른것을 호출하게 된다.
```

### 정리
* @Bean만 사용해도 스프링 빈으로 등록은 되지만, 싱글톤 보장이 안된다.
* <b>크게 고민할 필요없이 스프링 설정 정보는 항상 @Configuration을 사용해서 싱글톤을 보장하자!</b>






