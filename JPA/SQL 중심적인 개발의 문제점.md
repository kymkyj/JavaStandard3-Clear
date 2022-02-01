[→ Open in Slid](https://slid.cc/docs/aa018a4bd70a418db57989e14742945d)


---


데이터베이스의 세계는 현재 아직 RDB(관계형 디비)가 잡고 있다.


즉 객체를 관계형 디비에 저장해서 관리한다.

- 문제점은 관계형 디비에 저장하다보니 SQL이 중요한 비중을 차지한다.

- 수정의 경우에도 SQL 수정을 위주로 해야하며, 모든 SQL을 짜야한다.




[![SQL 중심적인 개발의 문제점 image](https://slid-users-assets-v1-seoul.s3.ap-northeast-2.amazonaws.com/public/capture_images/aa018a4bd70a418db57989e14742945d/a5947314-8b76-40a6-9d6e-4c763eb7e6b3.png)](https://slid.cc/vdocs/aa018a4bd70a418db57989e14742945d?v=0c45f0a0e23d4ac0add41c3566b67441&start=248.827625)


ex) memberId와 name을 통해 쿼리문을 다 짜여진 상태로 개발이 완료가 되었으나, 이후에 전화번호(tel)를 추가해달라는 요청으로 컬럼도 추가해야하고 본질적인 쿼리문에도 수정작업이 들어가야한다.

- 이로인해 SQL에 의존적인 개발을 피하기 어렵다는 점이 큰 문제로 작용한다.





**패러다임의 불일치 문제 (객체 vs 관계형 데이터베이스)**

1. 객체지향이 나온 사상과 관계형 데이터베이스가 나온 사상 자체가 다르다.

2. 관계형 데이터베이스는 데이터를 정규화해서 보관하는 게 목적 vs 객체는 속성과 기능으로 이루어져있으며, 메서드 등을 캡슐화해서 사용 목적

- 결국 이 두개가 패러다임이 안맞는 데 이러한 객체를 관계형 데이터베이스에 넣으려다보니 문제가 발생하게 되는 것

- 결국에는 관계형 데이터베이스를 써야한다는 점인데, 쿼리를 작성해야하고 이런 작업을 모두 개발자가 해야한다. 개발자 = SQL매퍼





**상속(객체 vs 관계형DB)**

[![SQL 중심적인 개발의 문제점 image](https://slid-users-assets-v1-seoul.s3.ap-northeast-2.amazonaws.com/public/capture_images/aa018a4bd70a418db57989e14742945d/8966e4fc-74dc-45aa-8572-b6f05c913415.png)](https://slid.cc/vdocs/aa018a4bd70a418db57989e14742945d?v=0c45f0a0e23d4ac0add41c3566b67441&start=471.426874)

1. 객체에서의 상속관계 vs 테이블에서의 슈퍼타입 서브타입 관계

2. INSERT 까지는 문제가 없지만, 조회에서의 문제점이 발생한다.

3. ALBUM에 대한 데이터를 조회해오려면, ITEM과 조인을 해야하고 각각의 객체를 생성(ITEM에 맞는 것은 ITEM에 넣어주고, ALBUM에 관한 데이터는 ALBUM에 넣어주고 난 다음에 값을 가져와야한다.

4. 그래서 보통 DB에 저장할 객체에는 상속 관계를 안쓴다.





**연관관계 (객체 vs 관계형DB)**

[![SQL 중심적인 개발의 문제점 image](https://slid-users-assets-v1-seoul.s3.ap-northeast-2.amazonaws.com/public/capture_images/aa018a4bd70a418db57989e14742945d/58c091e9-1585-41db-b86c-d1f5025604ed.png)](https://slid.cc/vdocs/aa018a4bd70a418db57989e14742945d?v=0c45f0a0e23d4ac0add41c3566b67441&start=695.410009)

1. 객체는 참조를 사용 member.getTeam() **vs** 테이블은 외래 키를 사용

2. 객체는 Member -> Team으로 갈수 있으나 Team에서 Member로 갈수 없다 (단방향) **vs** 테이블은 Member 에서 Team으로 조인을 통해서 갈 수 있고 반대로도 조인해서 갈수 있다 (양방향)

3. 관계를 설정하여 아래와 같이 쿼리문을 작성하지만, 객체에서 이것을 가져오게 될 경우 Member라는 객체 선언, Team 객체 선언 후에 꺼내온 데이터를 Member에 넣어주고 반환해주는 일련의 번거로운 과정을 거쳐야 한다.

[![SQL 중심적인 개발의 문제점 image](https://slid-users-assets-v1-seoul.s3.ap-northeast-2.amazonaws.com/public/capture_images/aa018a4bd70a418db57989e14742945d/f2eb4d51-f57b-4903-b889-c3761773fca9.png)](https://slid.cc/vdocs/aa018a4bd70a418db57989e14742945d?v=0c45f0a0e23d4ac0add41c3566b67441&start=933.865333)





**객체 그래프 탐색**

- 자바에서는 쩜(.) 찍어서 이동할 수 있는 그런 형태 ex) .getTeam()

- 객체는 자유롭게 객체 그래프를 탐색할 수 있어야 하는데, 처음에 실행하는 SQL문으로 인해서 탐색 범위가 제한되다보니까 자유롭게 이동할 수 없는 문제가 있다.

[![SQL 중심적인 개발의 문제점 image](https://slid-users-assets-v1-seoul.s3.ap-northeast-2.amazonaws.com/public/capture_images/aa018a4bd70a418db57989e14742945d/bb9bd4c3-0b9d-41d9-8788-da611df3de4f.png)](https://slid.cc/vdocs/aa018a4bd70a418db57989e14742945d?v=0c45f0a0e23d4ac0add41c3566b67441&start=1086.287708)





**엔티티 신뢰 문제**

[![SQL 중심적인 개발의 문제점 image](https://slid-users-assets-v1-seoul.s3.ap-northeast-2.amazonaws.com/public/capture_images/aa018a4bd70a418db57989e14742945d/2dd372f4-073e-4707-8119-78fd05143bd3.png)](https://slid.cc/vdocs/aa018a4bd70a418db57989e14742945d?v=0c45f0a0e23d4ac0add41c3566b67441&start=1133.192583)

- member.getTeam()도 호출할 수 있고, getOrder()랑 getDelivery()도 호출 할 수 있구나라고 생각할 수 있지만 이것은 신뢰할 수 없는 문제이다.

- memberDAO라는 데에서 어떤 쿼리가 날라갔고 어떻게 데이터가 조립되었는지 확인하지 않는 이상은 신뢰하고 쓸수 없다는 점

- 이러한 점 때문에 대안으로 상황에 따라 동일한 조회 메서드를 여러개를 만들어야 한다. getMember(), getMemberWithTeam()...





**비교하기(관계형 디비에서 객체 다루기 vs 자바 컬렉션)**

[![SQL 중심적인 개발의 문제점 image](https://slid-users-assets-v1-seoul.s3.ap-northeast-2.amazonaws.com/public/capture_images/aa018a4bd70a418db57989e14742945d/3741e70a-3471-444f-a363-228786e20454.png)](https://slid.cc/vdocs/aa018a4bd70a418db57989e14742945d?v=0c45f0a0e23d4ac0add41c3566b67441&start=1238.394583)

- member1 == member2가 다른 이유는 MemberDAO에서 일반적인 SQL을 호출하고 값을 반환하기 때문에 같은 식별자를 주더라도 다르다.

[![SQL 중심적인 개발의 문제점 image](https://slid-users-assets-v1-seoul.s3.ap-northeast-2.amazonaws.com/public/capture_images/aa018a4bd70a418db57989e14742945d/f38a56dc-7df6-4ba9-90f6-a8e866e87205.png)](https://slid.cc/vdocs/aa018a4bd70a418db57989e14742945d?v=0c45f0a0e23d4ac0add41c3566b67441&start=1278.525666)

- 자바 컬렉션을 통해 같은 식별자를 넣게 되면, member1 == member2를 비교하면 참조하는 값이 같기때문에 같은 값이 된다.





**객체를 자바 컬렉션에 저장하듯이 DB에 저장할 수 없을 까? 라는 고민을 통해 나온 방법이 JPA 기술이다.**

---


[참조 링크](https://www.inflearn.com/course/ORM-JPA-Basic/lecture/21670?tab=curriculum&volume=1.00)





















