### @Configuration과 싱글톤
코드로 먼저 살펴보자!
``` java

@Configuration
public class AppConfig {

    // @Bean memberService -> new MemoryMemberRepository()
    // @Bean orderService -> new MemoryMemberRepository()
    // 이렇게 되면 MemoryMemberRepository를 두번 호출하는데 싱글톤패턴에 어긋나는게 아닌지 확인해봐야한다.

    @Bean
    public MemberService memberService(){
        return new MemberServiceImpl(memberRepository());
    }

    @Bean
    public MemberRepository memberRepository() {
        return new MemoryMemberRepository();
    }

    @Bean
    public OrderService orderService(){
        return new OrderServiceImpl(memberRepository(), discountPolicy());
    }

    @Bean
    // AppConfig = 공연기획자 를 통해 할인정책을 바꾸더라도 이부분을 변경해야 한다.
    public DiscountPolicy discountPolicy() {
//        return new FixDiscountPolicy();
        return new RateDiscountPolicy();
    }

```
* memberService 빈을 만드는 코드를 보면 memberRepository()를 호출
  * 이 메서드를 호출하면 new MemoryMemberRepository()를 호출
* orderService 빈을 만드는 코드도 동일하게 memberRepository()를 호출하고 new MemoryMemberRepository() 호출
* 결과적으로 new MemoryMemberRepository 가 생성되면서 싱글톤이 꺠지는 것 처럼 보인다.

----

### 테스트 및 정리
<img src = https://user-images.githubusercontent.com/32288986/128882029-78ad4ac1-7450-40f0-8aa6-036c42e467c4.png>
* 위 이미지에서 보면 실제 출력될것이다 라고 추측한 횟수랑 다른 결과값을 보여주고 있다.
* 예상으로는 memberRepository를 세번 불러야하는데 한번만 메서드를 호출한다.
* 이렇게 된 이유에 대해서는 다음 장에서 정리하겠다!

```
    /* 예상 출력순서 */
    // call AppConfig.memberService
    // call AppConfig.memberRepository
    // call AppConfig.memberRepository
    // call AppConfig.orderService
    // call AppConfig.memberRepository
    
    /* 실제 스프링에서 출력해주는 순서 */
    // call AppConfig.memberService
    // call AppConfig.memberRepository
    // call AppConfig.orderService
    
```
