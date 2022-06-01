### AWS EC2에 Mysql(DB)설치하기
 - EC2에 Mysql 설치하는 방법으로는 yum 패키지 자체적으로 지원하는 mysql로는 설치할 수 없다.
 - 자세히 말하자면 이제는 지원하지 않는 듯 하다.
 - 설치를 하기 위해서는 현재시점에서 최신 mysql버전을 확인한다.
 - 아래의 명령어를 통해 현재 나의 linux 버전에 맞는 mysql을 다운로드 및 설치를 진행한다.
 - sudo yum localinstall https://dev.mysql.com/get/mysql80-community-release-el7-3.noarch.rpm

위의 명령어로 설치를 진행하고 난 후에 서버를 별도로 설치해준다.
 - sudo yum install mysql-community-server

#### 참조url : https://goddaehee.tistory.com/292


### mysql 설치시 발생하는 오류 및 대처 정리
-- 아래와 같은 메시지가 나온다면..
Is this ok [y/d/N]: y

****
Downloading packages:

warning: /var/cache/yum/x86_64/2/mysql80-community/packages/mysql-community-client-8.0.28-1.el7.x86_64.rpm: Header V4 RSA/SHA256 Signature, key ID 3a79bd29: NOKEY

Retrieving key from file:///etc/pki/rpm-gpg/RPM-GPG-KEY-mysql

The GPG keys listed for the "MySQL 8.0 Community Server" repository are already installed but they are not correct for this package.

Check that the correct key URLs are configured for this repository.

 Failing package is: mysql-community-client-8.0.28-1.el7.x86_64

 GPG Keys are configured as: file:///etc/pki/rpm-gpg/RPM-GPG-KEY-mysql****
****

 아래와 같은 명령어를 먼저 수행한 후에 다시 yum을 실행한다.
 - sudo rpm --import https://repo.mysql.com/RPM-GPG-KEY-mysql-2022
 - 위 명령어 실행 후 다시 실행 하는 yum 명령어 : sudo yum install mysql-community-server

참조 url : https://blog.daum.net/kiostory/281

****
ERROR 1820 (HY000): You must reset your password using ALTER USER statement before executing this statement.
****
 - mysql 접속 후 위와같은 메시지가 뜬다면
 - 처음에 root 계정의 비밀번호가 임시적으로 생성되어있으므로 바꿔주는 작업을 먼저하라는 메시지이다.

****
root 비밀번호 변경후 사용하라고해서 변경
비번 조건이 까다로움(대소문자숫자특수문자조합일때만 변경가능)
- 내부 로컬 접속만 허용시
ALTER USER 'root'@'localhost' IDENTIFIED BY 'Whdcentos12!@';
- 외부 모든 접속 허용시
ALTER USER 'root'@'%' IDENTIFIED BY 'Whdcentos12!@';
****
