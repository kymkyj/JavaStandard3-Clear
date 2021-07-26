### AppConfig 리팩터링

``` java

// 애플리케이션 전체를 설정하고 운영하는 녀석
/*
    AppConfig 리팩토링
    asis : 메서드 명만 봤을 떄 역할이 드러나지 않았다.
    tobe : 메서드 명만가지고도 어떤역할인지 확연히 구분되며 서비스부분과 Repository 부분이 구분된다.
 */
public class AppConfig {

    public MemberService memberService(){
        return new MemberServiceImpl(memberRepository());
    }

    private MemberRepository memberRepository() {
        return new MemoryMemberRepository();
    }

    public OrderService orderService(){
        return new OrderServiceImpl(memberRepository(), discountPolicy());
    }

    public DiscountPolicy discountPolicy() {
        return new FixDiscountPolicy();
    }
}


```
