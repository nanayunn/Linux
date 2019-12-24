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
1. 

***

### 명령어 연습하기

> 현업에서는 UI가 없는 화면에서 리눅스를 이용하기 때문에
>
> gedit(편집 명령어) 대신 vi 명령어를 이용하자

- UI 화면 설정
  - `Ctrl`+`Alt`+`F5` : UI가 없는 검정 터미널 화면
  - `Ctrl`+`Alt`+`F1` : UI가 설정된 화면으로 돌아가기
- `su`  : (Switch User)
- `su - ` : 사용자 뿐만 아니라 환경까지 이동(변경 후 변경된 사용자의 홈으로 이동)
- `history -c` : 명령어 내역 삭제 

vi 에디터 실행 `=>` 명령 모드 `=>` `esc` 키를 통해 **입력 모드**와 **라인 명령모드**를 번갈아가며 쓸 수 있다.

|            키             | 설명                                                         |
| :-----------------------: | ------------------------------------------------------------ |
|             i             | 입력모드, 현재 커서의 앞에 입력                              |
|             a             | (append)현재 커서의 뒤에 입력                                |
|             o             | 현재 커서의 다음 줄에 입력                                   |
|             s             | 현재 커서 위치의 한 글자를 지우고 입력                       |
|             I             | 현재 커서의 줄 맨 앞에서 입력                                |
|             A             | 현재 커서의 줄 맨 마지막에서 입력                            |
|             O             | 현재 커서의 이전 줄에 입력                                   |
|             S             | 현재 커서의 한 줄을 지우고 입력                              |
|          h,j,k,l          | 순서대로 `←` `↓` `↑` `→`                                     |
|            gg             | 제일 첫 행으로 이동                                          |
|             G             | 제일 끝 행으로 이동                                          |
|      :(숫자)`enter`       | 해당 숫자의 행으로 이동                                      |
|         :`set nu`         | 각 행마다 숫자가 표시되도록 함                               |
|            cw             | `" "` 속의 내용을 삭제(커서의 위치를 포함한 뒷부분의 내용이 삭제됨) |
|             u             | 되돌리기                                                     |
|         `Ctrl`+R          | 다시하기                                                     |
|        `shift`+`~`        | 대소문자 변경                                                |
|             x             | 커서가 위치한 글자 삭제                                      |
|             X             | 커서가 위치한 앞 글자 삭제                                   |
|            dd             | 현재 커서의 행 삭제                                          |
|         (숫자)dd          | 숫자만큼의 행 삭제                                           |
|            yy             | 현재 커서가 있는 행을 복사                                   |
|         (숫자)yy          | 숫자만큼의 행 복사                                           |
|             p             | 복사한 내용을 현재 행 이후에 붙여넣기                        |
|             P             | 복사한 내용을 현재 행 이전에 붙여넣기                        |
|           `:`q!           | 편집한 내용을 저장하지 않고 종료                             |
| `:%s/기존문자열/새문자열` | 문자열 치환하기                                              |

