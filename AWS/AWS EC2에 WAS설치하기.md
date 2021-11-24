## AWS EC2에 WAS 설치하기
 - Tomcat설치를 기준으로 한다.
 - Tomcat 홈페이지에서 다운받을 버전의 링크를 복사한다.
 - wget 명령어를 통해서 해당 링크를 통해 톰캣을 다운받는다.
 - 압축을 풀고 원하는 디렉토리에 톰캣을 위치시킨다.
 - vi /etc/profile 을 열어서 환경설정을 잡아준다.
 - 실행방법은 톰캣경로에 bin 아래에 있는 startup.sh / shutdown.sh로 동작시킨다.
