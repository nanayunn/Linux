# Linux

### 설치 및 환경설정

1. vmware Workstation player 무료 버전

2. `C:\Program Files (x86)\VMware\VMware Player`

   >  `vmnetcfg` 파일 설치 및 실행을 통해 IP 주소 변경 가능

3. 변경 주소는 192.168.111.1



### 가상의 컴퓨터 생성

1. create a new Virtual Machine

2. Linux//CentOS 7 64-bit

3. Edit virtual machine settings 

   - memory 4GB
   - Processer(늘리면 빨라짐) 8
   - CD/DVD CentOS 설치 CD 삽입 후 후에 제거

4. 가상의 브라우저 환경설정

   1. 키보드 : 한국어/영어(미국)

   2. 소프트웨어 : 개발 및 창조를 위한 워크 스테이션

   3. 네트워크 및 호스트 이름 : 활성화

   4. 설치 대상 : 파티션을 설정합니다.

      - 표준 파티션 선택

      - (추가) swap/2G

        > 하드디스크의 2GB를 메모리화 하겠다

      - (추가) `/`/ (메모리 자동 설정) : root 설정

   5. 설치 중 Root와 사용자 설정

      - root/111111(관리자)
      - centos/111111

   6. 라이센스 정보 동의

   7. Kdump 비활성화

5. 업데이트 비활성화

   1. 시스템 도구 `->` 소프트웨어

      > `최신 패키지만` **비활성화**

   2. 시스템 도구 `->`  소프트웨어 공급원

      > `업데이트 확인` **하지 않기**

   3. YUM 명령 중 업데이트 비활성화

      > *YUM이란?*
      >
      > - CentOS 소프트웨어를 설치할 때 사용하는 명령어

      1. `cd /etc/yum.repos.d/` (폴더 이동)

      2. `ls` (파일 확인)

      3. `gedit CentOS-Base.repo`

         `gedit CentOS-Source.repo`  (파일 편집)

      4. `#`released updates 항목 지워주기

      5. `mv CentOS-Base.repo CentOS-Base.repo.bak` (기존 저장소 백업)

      6. `wget http://download.hanbit.co.kr/centos/7/CentOS-Base.repo` (새 저장소 다운로드)

      7. `chmod` 644 *(권한 변경)

      8. `rm  *.repo~` (repo~가 딸린 필요없는 파일들 삭제)

      9. `yum clean all` (저장소 초기화)

   4. IP 주소 변경

      1. `cd /etc/sysconfig/network-scripts/`

      2. `ls`

      3. `gedit ifcfg-xxxxxxx`(ls로 확인한 파일 편집)

      4. 파일 편집으로 Server에 고정IP 할당

         - BOOTPROTO=none
         - IPADDR=192.168.111.100
         - NETMASK=255.255.255.0
         - GATEWAY=192.168.111.2
         - DNS1=192.168.111.2

      5. 설정 내용 적용 명령어 실행

         > `systemctl restart network`
         >
         > 이후 `ifconfig`로 변경된 IP 확인

      6. 보안 설정 해제

         > `gedit /etc/sysconfig/selinux`
         >
         > SELINUX='disabled'

      7. host 이름 설정

         > `hostname` (해당 서버의 이름 확인)
         >
         > `hostnamectl set-hostname server1`(해당 서버의 이름을 server1로 바꾸겠다)
         >
         > `gedit /etc/hosts`(해당 서버가 다른 IP 주소를 가진 서버를 인식할 수 있도록 IP주소와 서버이름 입력)

      `ping (서버이름)` `->` (서버이름)에게 응답 요청하는 것

***

### Server Clone 설정하기



1. 이미 만든 server의 파일 복사, 붙여넣기
2. 폴더의 configuration 파일의 displayName을 원하는 서버 이름으로 변경
3. Open Virtual machine : 복사한 서버 열어주기
4. Virtual machine setting : Network Adapter->> macAddress(generate 하기)
5. 서버 실행(I moved it 선택)
6. IPADDRESS 변경
7. hostname 변경