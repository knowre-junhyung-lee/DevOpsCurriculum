# Quest 01. 리눅스와 친해지기

## Introduction
* 이번 퀘스트를 통해 리눅스의 기본적인 구조와 기능에 대해 공부할 수 있습니다.

## Topics
* 리눅스의 기본 커맨드
  * `cd`, `pwd`, `ls`, `cp`, `mv`, `mkdir`, `rm`, `touch`, `ln`, `echo`, `cat`, `tail`, `find`, `ps`, `kill`, `grep`, `wc`, `df`, `du`
  * 파이프(`|`) 문자
* 리눅스의 기본적인 디렉토리 구성
  * `/bin`, `/usr/bin`, `/boot`, `/dev`, `/etc`, `/home`, `/lib`, `/mnt`, `/proc`, `/root`, `/sbin`, `/usr/sbin`, `/tmp`, `/usr`, `/var`
* 쉘과 환경변수와 퍼미션
  * sh, bash, zsh
  * `.bash_profile`, `.bashrc`, `.zshrc`
  * `env`, `set`, `unset`, `export`
  * `chmod`, `chown`, `chgrp`
  * setuid, Sticky bit
* 운영체제의 기초
  * 프로세스와 쓰레드
  * 파일 시스템
* 리눅스의 배포판
  * Ubuntu, Debian, Redhat Enterprise, CentOS, Gentoo, Amazon Linux
  * 패키지 시스템: `apt`(.deb), `yum`(.rpm)
* vi
  * `i`, `w`, `q`, `u`, `d`, `p` 명령

## Resources
* [The Linux command line for beginners](https://ubuntu.com/tutorials/command-line-for-beginners#1-overview)
* [The Linux Directory Structure, Explained](https://www.howtogeek.com/117435/htg-explains-the-linux-directory-structure-explained/)
* [Unix / Linux - What is Shells?](https://www.tutorialspoint.com/unix/unix-what-is-shell.htm)
* [zsh](https://github.com/ohmyzsh/ohmyzsh/wiki/Installing-ZSH)
* [About systemd](https://www.infoworld.com/article/2832405/what-is-systemd-and-why-does-it-matter-to-linux-users.html)
* [About linux distributions](https://thebloggingpot.com/2018/05/23/different-linux-distributions-explained/)
* [RPM and YUM package management](https://developer.ibm.com/technologies/linux/tutorials/l-lpic1-102-5/)
* [File editing with vi](https://developer.ibm.com/technologies/linux/tutorials/l-lpic1-103-8/)

## Checklist
* 리눅스의 파이프 문자는 어떤 역할을 하나요?
  * 프로세스의 출력을 다른 프로세스의 입력으로 사용하기 위해서 사용합니다. 
* 리눅스의 셸은 어떤 역할을 하나요? bash와 zsh는 어떻게 다른가요?
  * 리눅스의 셸은 명령줄 인터페이스의 일종입니다. 사용자들이 직접 컴퓨터의 기계어를 작성하여 사용하기 어렵기 때문에 OS 유틸리티, 명령어 등 을 찾아서 실행할 수 있도록 하고 환경변수 설정이나 작업을 자동화할 수 있는 스크립트를 작성할 수 있도록 기능을 제공합니다.
Bash 와 zsh의 차이는 확장 기능에 대한 제공입니다. Zsh 은 bash 에서 제공하는 대부분의 기능에 더하여 맞춤법 수정, 플러그인 추가, 별칭 등의 옵션을 선택할 수 있습니다.
* 리눅스의 권한 체계는 어떻게 이루어져 있나요?
  * 리눅스의 권한은 크게 유저와 그룹으로 이뤄져 있습니다.
유저의 id 인 uid, 그룹의 id 인 gid 에 따라서 파일에 대한 권한을 확인합니다.
각 파일은 uid, gid, 그 외 유저들에 대한 rwx 권한 즉 읽기, 쓰기 ,실행 권한을 설정할 수 있습니다.
* 프로세스와 쓰레드는 무엇인가요?
  * 프로세스는 메모리에 로드되어 실행중인 프로그램입니다.
프로그램이 실행되는 단위로 코드영역, 데이터 영역, 스택 영역, 힙 영역 등 을 할당받아서 실행되는 주체입니다.
이러한 프로세스는 1개이상의 스레드를 포함하고 있습니다. 
스레드란 실행의 흐름을 이르는 말입니다. 프로세스 의 데이터 영역과 코드영역, 힙 영역을 공유하고 개별의 스택영역을 가지고 있어 cpu 에서 실행 될 수 있는 최소한의 컨택스트를 갖추고 있습니다. 
멀티 코어 또는 멀티 프로세서 환경에서 개별로 실행될 수 있기때문에 병렬성을 요구하는 프로그램에 적합합니다.
* 현재 실행되고 있는 프로세스들 중 PID가 1인 프로세스는 어떤 역할을 할까요? init과 systemd는 무엇이고 어떻게 다른가요?
  * 먼저 공통점으로 init 과 systemd 모두 OS 를 부팅하면서 실행 되야하는 프로그램들을 실행시키는 부모 프로세스 역할을 합니다.
	차이점으로는 자식 프로세스들을 실행시키는 방식입니다. init 프로세스는 init.d 에 존재하는 스크립트 및 실행 파일을 순차적으로 실행합니다. 이러한 방식은 부팅 시 속도가 느려질 수 있고 병렬적으로 실행하지 못 한다는 단점이 있습니다. 하지만 systemd 에서는 부팅 시 시작되야 하는 것 들을 병렬적으로 실행하고 스크립트가 아닌 구성 파일을 통해 명령을 실행시킵니다.
* 파일시스템이란 무엇일까요? 어떤 것이 있을까요? 지금 다루는 운영체제는 어떤 파일시스템을 쓰고 있나요?
  * 파일시스템이란 디스크와 같은 영구적 저장장치에 파일을 저장하기 위해 발명된 시스템입니다.
파일은 이진데이터를 나열해 놓은 것인데 이 파일을 저장할 때 저장장치의 형식에 따라서 저장하고 효율적으로 관리할 수 있도록 한 일종의 자료 저장 방식입니다.
파일시스템의 종류로는 리눅스 게열의 ext3,4 , xfs, zfs, jfs, ntfs, apfs 등 이 있습니다. 
일반적인 리눅스 서버에서는 xfs 를 많이 사용하고 현재 사용중인 Mac OS 에서는 apfs 를 사용하고 있습니다.
* 리눅스의 배포판이란 무엇일까요? 여러 가지 배포판들은 어떻게 생겨났을까요?
  * 리눅스 배포판은 리눅스 커널을 베이스로 사용자들이 편하게 사용할 수 있도록 여러가지 유틸리티 등 을 개발하여 커스터 마이징한 os 패키지입니다. 최초의 리눅스는 하드웨어를 관리하는 커널만 존재하였지만 GNU 프로젝트에서 이를 사용해 여러가지 도구들을 개발하고 오픈소스로 공개함으로서 커스터마이징된 수많은 배포판이 탄생하였습니다.
* 리눅스의 패키지 시스템이란 무엇일까요? 이러한 시스템이 생긴 이유는 무엇일까요? deb과 rpm은 어떤 차이가 있을까요? RPM이 있는데 yum과 같은 시스템이 나온 이유는 무엇일까요?
  * 리눅스의 패키지 시스템은 오픈소스로 공개된 여러 소프트웨어를 사용자가 직접 컴파일하여 사용하기 어려운 점 때문에 생겨났습니다. 패키징된 바이너리를 실행 함으로써 소프트웨어를 자동으로 설치하고 사용할 수 있도록 한 것 입니다. 리눅스의 여러 배포판 중에 대표적으로 데비안 계열의 deb 파일 ,레드헷 계열의 rpm 등이 있습니다.
이렇게 생긴 패키징 시스템으로 편리한 사용이 가능해졌지만 소프트웨어 의존성에 대한 문제가 해결되지 않았습니다.
소프트웨어 의존성에 대한 패키지 정보를 자동으로 찾아서 필요한 rpm 파일들을 모두 설치해주는 시스템의 예가 바로 yum 입니다.
* vi는 어떤 에디터인가요? vi와 vim은 어떻게 다를까요? vi는 왜 모든 리눅스의 기본 에디터가 되었을까요?
  * vi 는 CLI 환경에서 문서를 편집하기위한 에디터입니다. vi 와 vim 은 모두 문서편집 기능을 가지고 있지만 vim 은 사용성을 향상 시켰습니다. Vim 은 문법 강조와 유닉스가 아닌 여러 플랫폼환경에서도 사용이 가능합니다.
이러한 vi 에디터를 리눅스에서 사용하는 이유는 편리성 때문입니다. 리눅스는 GUI 로도 사용이 가능하지만 대부분 CLI 환경으로 많이 사용합니다. CLI 환경에서는 마우스를 사용할 수 가 없기 때문에 키보드를 기반으로 여러가지 기능을 사용할 수 있는 vi 에디터를 사용하기에 적합합니다.

## Quest
* 인스턴스 생성
  * t3.nano 등급으로 EC2 인스턴스를 생성해 봅시다! Amazon Linux 2, Ubuntu 두 가지를 각각 생성해 봅니다.
  * EC2 생성 과정에서 .pem 파일이 하나 생기는데, 이는 저에게 슬랙을 통해 공유해 주시면 됩니다.
  * 세 배포판은 어떻게 다른가요?
* 리눅스 연습
  * Amazon Linux 2 인스턴스에서 위의 Topics의 기본 커맨드를 연습해 봅니다.
  * 리눅스의 기본 디렉토리들에 어떤 정보들이 있는지 둘러 봅니다.
  * zsh를 설치하고 `.zshrc` 파일을 포함해 여러 가지 설정을 해 봅니다.
  * Topics의 환경변수나 퍼미션 관련 커맨드를 연습해 봅니다.
  * 현재 실행되고 있는 프로세스들과 마운트 된 파일시스템들을 확인해 봅니다.
  * vi를 열어 여러 가지 기본 명령과 간단한 편집 방법을 연습해 봅니다.
* 생성한 인스턴스 중 Ubuntu는 완전히 종료(Terminate)하고, Amazon Linux 2는 일단 꺼둡니다.

## Advanced
* 리눅스 외의 POSIX 호환 운영체제에는 어떤 것들이 있을까요? 그러한 운영체제들은 어떤 용도로 쓰일까요?
  * Mac OS, 솔라리스 등 이 있습니다. Mac OS 는 맥킨토시 게열의 컴퓨터에서 사용되고 솔라리스는 주로 SUN 사의 서버 컴퓨터 OS 용으로 사용됩니다.
* 윈도우를 제외하고, 최근에 발표된 운영체제들 중 POSIX에 호환되지 않는 운영체제도 있을까요?
  * 모바일에서 사용되는 리눅스 계열의 안드로이드가 있습니다. POSIX 기준을 만족시키려고 했지만 완벽한 호환은 아닙니다.
