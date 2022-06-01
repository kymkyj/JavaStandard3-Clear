### aws linux 정보 확인 명령어
 - grep . /etc/*-release
 - 위 명령어를 사용하면, 아마존 리눅스 버전 정보가 나타난다. 아마존 리눅스 2를 사용하고 있는 것을 알 수 있다.
 -  /etc/os-release:NAME="Amazon Linux"
    /etc/os-release:VERSION="2"
    /etc/os-release:ID="amzn"
    /etc/os-release:ID_LIKE="centos rhel fedora"
    /etc/os-release:VERSION_ID="2"
    /etc/os-release:PRETTY_NAME="Amazon Linux 2"
    /etc/os-release:ANSI_COLOR="0;33"
    /etc/os-release:CPE_NAME="cpe:2.3:o:amazon:amazon_linux:2"
    /etc/os-release:HOME_URL="https://amazonlinux.com/"
    /etc/system-release:Amazon Linux release 2 (Karoo)
    
 - 리눅스 커널 버전 확인 명령어
 - uname -r
