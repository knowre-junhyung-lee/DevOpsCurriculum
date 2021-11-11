# Quest 09. 정적인 컨텐츠 서비스 하기

## Introduction
* 이번 퀘스트를 통해 정적인 컨텐츠의 서비스와 CDN의 개념, 그리고 HTTP 캐싱에 대해 알아보겠습니다.

## Topics
* S3
* Cloudfront
* HTTP Cache
* CORS
* Invalidation(Purging)

## Resources
* [Amazon S3](https://aws.amazon.com/ko/s3/)
* [콘텐츠 전송 네트워크(CDN)](https://www.akamai.com/ko/our-thinking/cdn/what-is-a-cdn)
* [Amazon Cloudfront](https://aws.amazon.com/ko/cloudfront/)
* [HTTP caching](https://developer.mozilla.org/ko/docs/Web/HTTP/Caching)
* [교차 출처 리소스 공유 (CORS)](https://developer.mozilla.org/ko/docs/Web/HTTP/CORS)


## Checklist
* AWS의 S3는 어떤 서비스일까요?
  * 파일을 저장할 수 있는 스토리지 서비스입니다.
버킷이라는 단위로 서비스를 관리하고 버킷안에 파일이 객체로 저장됩니다.
S3 는 클래스로 나누어져 있고 클래스 별로 속도, 가용성, 비용의 차이가 있습니다.
S3 는 대표적으로 정적 웹사이트 호스팅, 버젼관리가 필요한 파일 저장에 사용됩니다.

* AWS의 Cloudfront는 어떤 서비스일까요?
  * Cloudfront 는 CDN 서비스의 일종입니다.
CDN 서비스를 위해서 여러 엣지 서버가 전 세계에 배치되어 있고 해당 서버들은 원본 데이터를 캐싱하고 있습니다.
이 엣지 서버들을 이용하여 최대한 근접해 있는 서버를 통해 콘텐츠를 이용할 수 있도록 합니다.

* HTTP의 캐싱은 어떤 식으로 이루어질까요?
  * 클라이언트가 처음 정적파일들을 서버에 요청하고 그 파일을 내부에 저장합니다.
캐싱을 유지하는 시간은 HTTP cache-control 헤더를 통해 서버가 클라이언트에게 전달합니다.
클라이언트는 이후 같은 요청을 진행 할때 먼저 서버에게 정적 파일이 변한 점이 있는지 확인합니다.
변한점이 있다면 서버에게 재요청을 하고 변한 점이 없다면 클라이언트는 캐싱된 파일을 사용합니다.

* CORS는 무엇인가요? 어떤 헤더를 통해 구현되나요? EC2 서버나 S3에 구현하려면 어떻게 해야 할까요?
  * CORS 는 클라이언트가 자신의 도메인이 아닌 곳에 요청을 보내면 해당 요청이 블록되는 현상입니다.
HTTP Access-Control-Allow-Origin 헤더를 통해서 허용할 도메인에 대한 정보를 보내줍니다.
EC2 서버에서 실행 중인 어플리케이션이 CORS 를 허용하는 헤더를 함꼐 응답하도록 합니다.
S3 에서는 버킷정책을 생성하면 됩니다. 허용할 도메인과 메소드 등의 정보를 JSON 파일로 작성하고 콘솔을 통해 설정해줍니다.

## Quest
* 만들어 둔 서버 API로부터 특정 정보를 받아 웹 서비스로 뿌려주는 클라이언트를 개발해 봅시다.
* 이를 S3에 배포하고, Cloudfront를 통해 서비스하는 인프라를 구성해 봅시다.
* 클라이언트를 수정 배포했을 때, 수정사항이 Cloudfront를 통해 최대한 빨리 반영되게 하려면 어떻게 해야 할까요?

## Advanced
* CDN은 어떤 기술일까요? 어떤 장점이 있을까요? 어떻게 구현되는 기술일까요?
* S3의 스토리지 클래스는 어떤 것이 있을까요? 이를 통해 어떤 응용을 할 수 있을까요?
