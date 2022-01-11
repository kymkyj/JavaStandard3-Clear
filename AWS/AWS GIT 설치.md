### AWS EC2에 git 설치하기

 - EC2에 git을 설치하는 방법은 간단하다.
 - yum이라는 명령어를 통해 git 설치가 가능하다.
 - yum은 Yello dog Updater, Modified의 약자로 RPM 기반의 시스템을 위한 자동 업데이터 겸 패키지 설치/제거 도구를 말한다.

## 설치방법
 1. 먼저 yum을 업데이트하여 최신화를 유지시킨다 (sudo yum update -y)
 2. git을 설치한다 (sudo yum install git -y)
 3. git 버전을 확인한다 (git version)
