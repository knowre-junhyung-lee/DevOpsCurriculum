# Quest 12. DNS와 HTTPS

## Introduction
* 이번 퀘스트에서는 DNS에 대한 더 깊은 이해와 함께, HTTPS와 TLS에 대해 알아보겠습니다.

## Topics
* DNS
* Route53
* HTTPS
* TLS
* Certificate Manager
* HTTP/3

## Resources
* [DNS Servers](https://www.redhat.com/sysadmin/dns-domain-name-servers)
* [What is DNS](https://aws.amazon.com/ko/route53/what-is-dns/)
* [Route 53](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/getting-started.html)
* [HTTPS protocol explained](https://anushadasari.medium.com/the-https-protocol-explained-under-the-hood-c7bd9f9aaa7b)
* [TLS](https://www.internetsociety.org/deploy360/tls/basics/)
* [AWS Certificate Manager](https://docs.aws.amazon.com/ko_kr/acm/latest/userguide/acm-overview.html)
* [HTTP3 explained](https://http3-explained.haxx.se/ko)

## Checklist
* DNS의 레코드에는 어떤 종류들이 있나요? 이 종류들은 어떤 용도로 쓰일까요?
  * A : 도메인 이름을 IPv4 와 연결합니다.
  * AAA : 도메인 이름을 IPv6 와 연결합니다.
  * CNAME : A레코드와 연결되는 별칭을 정의합니다.
  * NS : 도메인 영역에 해당하는 네임서버 정보를 제공합니다.
  * MX : 메일서버의 정보를 제공합니다.
  * PTR : 역방향 조회에서 A 레코드를 가리킵니다.
  * SOA : 도메인 영역의 주 DNS 서버와 기본 설정 값들을 정의합니다.
  
* Route53의 Alias 기능이란 무엇인가요?

  * DNS 레코드 중 CNAME 과 유사한 역할을 합니다.
하지만 AWS 내의 리소스와 Route53의 호스팅 영역 내에서만 가능합니다.
또한 CNAME 은 해당 도메인의 이름으로는 설정이 불가능하지만 Alias 에서는 가능합니다.

* 대부분의 최신 브라우저에서는 HTTP 대신 HTTPS가 권장됩니다. 이유가 무엇일까요?

  * HTTP 프로토콜은 보안에 취약하기 때문입니다. 정보를 평문으로 전달하고 메세지에 대한 신뢰성을 검증할 수 없습니다.
이 단점을 보완하기위해 HTTPS 를 사용하게 되었습니다.
대표적으로 크롬 브라우저에서는 http 프로토콜을 https 프로토콜로 리다이렉트하도록 설정되어있습니다.
또한 인증기관에 등록되지 않거나 신뢰할 수 없는 인증서를 사용하는 사이트에 대한 경고를 진행합니다.

* HTTPS와 TLS는 어떤 식으로 동작하나요? HTTPS는 어떤 역사를 가지고 있나요?

  * HTTPS 는 넷스케이프가 개발한 웹 프로토콜입니다. HTTP 의 보안을 강화하기위해 개발되었습니다.
  * HTTPS 프로토콜은 사용자가 HTTP 통신을 진행하기 전에 TLS 라는 보안 프로토콜을 통해 암호화와 메세지인증 설정을 합니다.
TLS 보안 협상을 위해서는 비대칭키와 대칭키 방식이 사용됩니다.
클라이언트와 서버 간에 데이터를 교환할때 사용하는 대칭키를 사전에 공유할 필요가 있습니다.
통신에 사용할 대칭키를 교환하기 위해 비대칭키를 사용합니다.
TLS 혐상에서 클라이언트는 서버의 공개키를 제공받습니다. 서버는 자신의 개인키로 대칭키를 암호화하여 클라이언트에게 전달합니다.
서버의 개인키로 암호화 한 대칭키를 서버의 공개키를 이용해 해독하면 상호 대칭키를 공유하게 됩니다.
이후 대칭키를 통해 트래픽을 암호화하고 메세지에 대한 인증을 위해 대칭키와 해쉬를 이용하여 메세지 검증코드를 덧붙여 통신합니다.
위와 같은 과정으로 협상이 완료된 보안 설정을 통해서 HTTP 요청과 응답을 교환하게되고 클라이언트와 서버 간의 정보가 보호됩니다.


* HTTPS의 서비스 과정에서 인증서는 어떤 역할을 할까요? 인증서는 어떤 체계로 되어 있을까요?

  * 인증서는 서버의 공개키와 도메인에 대한 정보를 담고 있습니다.
인증기관의 서명이 들어가 있어 해당 인증서가 정당한지의 여부를 브라우저에서 확인할 수 있습니다.
HTTPS 통신 과정에서 TLS 형상을 진행할 때 서버는 클라이언트에게 인증서를 전달합니다.
클라이언트는 제공받은 인증서를 검증하고 TLS 보안 협상을 진행합니다.

  * 인증서는 CA 라는 인증기관에서 발급합니다.
클라이언트는 알려진 인증기관의 공개키를 가지고 있습니다.
해당 공개키를 통해서 서버로 부터 제공받은 인증서의 서명을 검증합니다.
CA 로부터 서명된 서버의 인증서를 CA 의 공개키로 검증할 수 있다면 신뢰할 수 있다고 판단합니다.

 
* HTTP/3은 기존 버전과 어떻게 다를까요? HTTP의 버전 3이 나오게 된 이유는 무엇일까요?

  * 기존의 HTTP 프로토콜의 오버헤드(TCP 3way-handshake, HOLB) 를 줄이기 위함입니다.
HTTP/3 프로토콜은 기존 버젼에서 사용하던 TCP 대신 UDP 프로토콜을 사용합니다.
UDP 기반의 QUIC 라는 프로토콜 위에서 동작합니다.
TCP 에서 제공했던 신뢰성과 HTTPS 로 사용되었던 보안 기술이 QUIC 를 통해 구현되었습니다.
이로서 오버헤드가 적어 속도가 빠른 UDP 의 장점과 신뢰성,보안성을 모두 만족시켰습니다.
또한 TCP 와 HTTP 의 결합으로 인해서 발생했던 HOLB(Head of Line Blocking) 현상을 방지할 수 있습니다. 


## Quest
* `xxx.knowre.com`에 해당하는 커스텀 도메인을 하나 부여해 드리겠습니다. Route53을 활용하여 이 도메인의 자체 네임서버를 구축해 보세요.
* Cloudfront에 연결된 정적인 웹사이트와 ECS에서 서비스 되는 API 서버가 위 도메인으로 서비스 되도록 설정과 연결해 보세요.
* Certificate Manager를 통해 인증서를 만들어 보세요. 그리고 위 두 서비스가 HTTPS로 서비스될 수 있도록 바꿔 보세요.
* HTTP로 접속했을 때 HTTPS로 리다이렉트 되도록 설정해 보세요.

## Advanced
* DNS의 TTL은 무엇인가요? 실제 리얼 월드에서는 이 DNS의 TTL이 어떻게 동작하고 있을까요?
  * DNS 의 TTL 은 해당 DNS 레코드 결과값이 캐시에 저장되는 시간입니다.
주 도메인 서버의 TTL 값에 따라서 DNS 레코드가 캐시되기 때문에 DNS 관련 변경사항은 주의가 필요합니다.
일반 사용자의 PC 에 캐시되는 경우는 해당 사용자만 적용되기 때문에 영향도가 적습니다.
하지만 ISP 와 같은 네임서버는 많은 사람이 사용하기 때문에 영향도가 클 수 있습니다.
도메인의 특성에 따라서 TTL 값을 정하고 작업이 있다면 TTL 값을 사전에 조정하는 방법도 있습니다.

* 사용중인 OS에서 인정하는 Root CA에는 어떤 기관들이 있을까요? 만약 이 기관중 하나의 인증서 키가 유출된다면 어떤 일이 일어날까요?
  * Root CA 는 코모도, 시만텍, 고대디, 글로벌 사인 등 여러 기관이 있습니다.
이 기고나들 중 하나의 키가 유출된다면 해당 기관이 인증해주는 하위 인증서들 전체를 신뢰할 수 없게 됩니다.
해당 기관으로부터 인증서를 발급받은 사업자나 기관에도 보안 사고가 발생할 수 있습니다.
따라서 Root CA 기관은 철저한 보안이 필요합니다.
