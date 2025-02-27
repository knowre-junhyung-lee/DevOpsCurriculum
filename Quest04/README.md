# Quest 04. 나의 첫 웹 서비스

## Introduction
* 이번 퀘스트에서는 웹 서비스를 만드는 기초적인 방법과 구성에 대해 알아보겠습니다.

## Topics
* 데몬
* 포트와 소켓
* 프록시(리버스 프록시, 포워드 프록시)

## Resources
* [Daemon Process](https://www.quora.com/What-is-a-daemon-process-in-Linux)
* [Reverse Proxy](https://www.nginx.com/resources/glossary/reverse-proxy-server/)

## Checklist
* 서버 환경에서 데몬이란 무엇일까요? node.js 서버를 데몬으로 만들려면 어떻게 해야 할까요?
  * 데몬이란 백그라운드로 실행되면서 특정한 이벤트가 발생하면 깨어나 그에 적합한 대응을하는 프로세스의 한 종류입니다.
node.js 는 런타임 중에서 예상치 못한 예외가 발생하면 종료를 하게됩니다. 
이 문제를 해결하기 위해서 node.js 프로세스를 지속적으로 모니터링하며 프로세스를 되살려주는 소프트웨어가 필요합니다.
데몬 관련 라이브러리를 통해서 데몬화시키거나 pm2 라는 소프트웨어를 이용하여 node.js 를 모니터링 및 관리할 수 있습니다. 
* nginx와 같은 리버스 프록시 서버를 사용하는 이유는 무엇일까요?
  * 웹어플리케이션의 부하를 줄이기 위해서 입니다. 
TLS 인증, 정적인 파일 전송, 전송 데이터 압축 등의 업무로직에 포함되지 않지만 성능 향상에 도움이 되는 것들을 처리할 수 있습니다.
또한 웹서버가 앞단에서 여러대의 웹어플리케이션에 트래픽을 부하 분산할 수 있기 때문에 가용성 측면에서도 도움이 됩니다.

## Quest
* vi를 이용하여, node.js의 3000번 포트로 기본적인 웹서버를 만든 후 띄워 보세요.
* 로컬 머신을 통해 띄운 웹서버의 3000번 포트에 접속해 보세요. AWS 콘솔에서 보안 그룹을 조정하려면 어떻게 해야 할까요?
* 서버의 앞쪽에 nginx를 설치하여 80포트를 통해 외부로 서비스 해 보세요.
* 서버에 터미널 접속을 종료해도 서버가 뜰 수 있게 해 보세요.

## Advanced
* 리눅스 시스템의 PID 1번 프로세스는 무엇일까요? systemd와 init.d는 어떤 시스템이고 어떤 차이가 있을까요?
  * 리눅스의 버젼에 따라서 init 프로세스 또는 systemd 프로세스로 나누어집니다.
init.d 에서는 init 프로세스가 초기 스크립트를 실행 시킵니다. 각 런레벨에 해당하는 스크립트를 순차적으로 실행합니다.
systemd 에서는 스크립트를 systemd 문법에 적합한 형식으로 작성하고 설정함으로서 규격화된 서비스 제어가 가능합니다.
또한 init 프로세스와 달리 병렬적으로 스크립트를 실행함으로서 신속한 부팅이 가능해집니다.

* AWS의 보안 그룹 시스템은 어떻게 구성되어 있을까요? 일반적인 방화벽 시스템은 어떤 설정들이 가능할까요?
  * AWS 보안 그룹 시스템은 IP 와 PORT 기반으로 트래픽을 제어합니다.
보안그룹은 크게 인바운드와 아웃바운드로 나눠져 있습니다.
EC2 를 예로 들면 인바운드는 EC2 측으로 들어오는 트래픽에 대한 제어, 아웃바운드는 EC2 에서 나가는 트래픽에 대한 제어입니다.
각 바운드는 세부적인 규칙을 가지고 있습니다. 그 규칙의 형식은 다음과 같습니다.
    * 프로토콜의 종류 TCP,UDP 등
    * IP 버전
    * IP주소 CIDR 표기
    * PORT 범위
  * 이러한 사항들을 설정하여 특정 IP와 PORT 에 대한 접근을 제어할 수 있습니다.
보안성을 위해서는 허용된 트래픽 외에는 모든 트래픽을 허용하지 않는 화이트리스트 방식이 유리합니다.

