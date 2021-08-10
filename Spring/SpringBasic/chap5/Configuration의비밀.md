### @Configuration과 싱글톤
코드로 먼저 살펴보자!
``` java

@Configuration
public class AppConfig {

    // @Bean memberService -> new MemoryMemberRepository()
    // @Bean orderService -> new MemoryMemberRepository()
    // 이렇게 되면 MemoryMemberRepository를 두번 호출하는데 싱글톤이 깨지는것이 아니냐?

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
    // AppConfig = 공연기획자 를 통해 할인정책을 바꾸더라도 이부분만 바꾸면 된다.
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


