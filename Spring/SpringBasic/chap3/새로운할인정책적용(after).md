### 새로운 할인정책 적용
#### AppConfig가 적용되어 변경한다
* 사용영역의 코드는 변경할 필요없이 AppConfig 부분(구성 영역)만 고치면 된다.

``` java

// ... AppConfig 일부분
    
// AppConfig = 공연기획자 를 통해 할인정책을 바꾸더라도 이부분만 바꾸면 된다.
    public DiscountPolicy discountPolicy() {
//        return new FixDiscountPolicy();
        return new RateDiscountPolicy();
    }
}

```

* AppConfig 에서 할인정책을 담당하는 구현체를 변경함 (FixDiscountPolicy -> RateDiscountPolicy)
* 할인 정책을 변경해도 이제 구성영역을 담당하는 AppConfig에서만 변경하면 된다.
* 단, 구성 역할을 담당하는 AppConfig(공연 기획자)는 모든 사용영역의 공연참여자인 구현 객체를 모두 알아야 한다.
* 사용영역에 있는 코드들은 전혀 손대지 않는다는점이 효율적이다! 
