### AWS EC2에 Mysql(DB)설치하기
 - EC2에 Mysql 설치하는 방법으로는 yum 패키지 자체적으로 지원하는 mysql로는 설치할 수 없다.
 - 자세히 말하자면 이제는 지원하지 않는 듯 하다.
 - 설치를 하기 위해서는 현재시점에서 최신 mysql버전을 확인한다.
 - 아래의 명령어를 통해 현재 나의 linux 버전에 맞는 mysql을 다운로드 및 설치를 진행한다.
 - sudo yum localinstall https://dev.mysql.com/get/mysql80-community-release-el7-3.noarch.rpm

위의 명령어로 설치를 진행하고 난 후에 서버를 별도로 설치해준다.
 - sudo yum install mysql-community-server

## 참조url : https://goddaehee.tistory.com/292

