# Quest 18. 서비스의 운영 (2): 로깅과 Elasticsearch

## Introduction
* 이번 퀘스트에서는 서비스의 운영을 위해 로그를 스트리밍하는 법에 대해 다루겠습니다.

## Topics
* ElasticSearch
* AWS ElasticSearch Service
* Grafana

## Resources
* [ElasticSearch](https://www.elastic.co/kr/what-is/elasticsearch)
* [ElasticSearch 101](https://www.elastic.co/kr/webinars/getting-started-elasticsearch)
* [Grafana Panels](https://grafana.com/docs/grafana/latest/panels/)

## Checklist
* ElasticSearch는 어떤 DB인가요? 기존의 RDB와 어떻게 다르고 어떤 장단점을 가지고 있나요?
  * ElasticSearch는 오픈소스 분산 검색 엔진입니다. 대량의 데이터를 저장, 검색, 분석할 수 있습니다.
공통점으로 기존의 RDBMS 도 데이터의 검색, 저장, 분석이  SQL 을 통해서 가능하다는 점입니다.
차이점은 다음과 같습니다.
  * 첫번째, ElasticSearch는 텍스트 검색과 분석에 특화되어 있습니다. RDBMS와 달리 역색인을 통해서 검색하고자 하는 텍스트에 대응하는 레코드 정보를 찾습니다.
  * 두번째, 분산형 구조를 적극 활용합니다. 대량의 데이터를 검색, 분석할 시 분산된 스토리지를 통해 속도의 이점을 가집니다.
  * 세번째, 관계형 구조가 아니기 때문에 구조의 제약이 적어 대용량, 비정형 데이터에 적합합니다.
  * 네번째, REST API 를 지원하여 범용적인 HTTP 형식으로 사용할 수 있습니다.
  * 다섯번째, RDBMS 와 달리 트랜잭션과, 롤백 기능을 제공하지 않습니다.
  
* AWS의 ElasticSearch Service는 어떤 서비스인가요? ElasticSearch를 직접 설치하거나 elastic.co에서 직접 제공하는 클라우드 서비스와 비교하여 어떤 장단점이 있을까요?
  * AWS의 ElasticSearch Service는 관리형 서비스입니다.
  * 설치형과 달리 버그,보안 픽스에 대한 업그레이드가 필요하지 않습니다.
  * elastic.co 에서 제공하는 서비스도 역시 관리형이지만 신규 배포를 생성할 시 항상 최신버전을 사용합니다.
  * AWS ElasticSearch에서는 다양한 버젼의 클러스터를 제공합니다. 
  * AWS 의 IAM을 통한 접근제어와 SAML, LDAP 등 다양한 보안 기능을 제공합니다.
  * VPC와 연동하여 클라우드 내부에서 사용이 가능합니다.
  
* Grafana의 Panel 형식에는 어떤 것이 있을까요? 로그를 보기에 적합한 판넬은 어떤 형태일까요?
  * Grafana 에는 대표적으로 Graph, Stat, Logs, Gauge, Table 등 이 있습니다.
로그는 Logs 판넬을 통해서 텍스트로 로그의 내용을 확인하는 방법이 적합합니다.
또한 로그의 내용을 기반으로 다른 판넬을 구성하여 데이터를 시각화할 수 있습니다.

## Quest
* 우리의 웹 서버, S3, Cloudfront, VPC, ELB 등이 로그를 남기도록 해 보세요.
* ElasticSearch Service 클러스터를 작은 사양으로 하나 만들고, 이 로그가 ElasticSearch로 들어가도록 해 보세요.
* Grafana를 이용해 ElasticSearch의 로그를 실시간으로 볼 수 있는 페이지를 만들어 보세요.

## Advanced
* ElasticSearch와 Grafana는 어떤 라이센스로 배포되고 있을까요? AWS와 같은 클라우드 제공자들이 이러한 오픈소스를 서비스화 하는 것을 둘러싼 논란은 어떤 논점일까요?
  * 기존의 ElasticSearch 는 오픈 소스로 운영 되었습니다.
하지만 Elastic 과 AWS의 분쟁으로 인해서 라이센스 정책이 달라지게 되었습니다.
  * Apache 2.0 라이센스로 운영 되던 중 AWS 에서 Elastic 의 독점 코드를 우려하여 Open Distro for Elasticsearch 를 공개하였습니다.
  * Elastic 은 이에 대응하여 SSPL과 Elastic 라이센스로 변경하겠다고 발표했습니다.
이로 인해서 결과적으로 Elasticsearch 는 오픈소스가 아니게 되었습니다.

  * AWS Elasticsearch = Apache 2.0
  * Elasticsearch = SSPL or Elastic
  * Grafana 의 라이센스는 현재 AGPLv3 입니다. AGPLv3 는 오픈소스로 인정된 라이센스입니다.
