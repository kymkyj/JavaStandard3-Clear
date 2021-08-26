### AppConfig 리팩터링

``` java

// 애플리케이션 전체를 설정하고 운영하는 녀석
/*
    AppConfig 리팩토링
    as-is : 메서드 명만 봤을 떄 역할이 드러나지 않았다.
    to-be : 메서드 명만가지고도 어떤역할인지 확연히 구분되며 서비스부분과 Repository 부분이 구분된다.
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

* new MemoryMemberRepository() 부분이 중복 제거 되었음 
    * MemoryMemberRepository를 다른 구현체로 변경할 때 한부분만 변경
* AppConfig 를 보면 역할과 구현 클래스가 한눈에 들어온다.
