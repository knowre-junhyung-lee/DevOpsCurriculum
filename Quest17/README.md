# Quest 17. 서비스의 운영 (1): 서버 들여다 보기

## Introduction
* 이번 퀘스트에서는 서비스 운영을 위한 리눅스 커맨드와 모니터링에 대해 다루겠습니다.

## Topics
* 리눅스의 커맨드들: `lsof`, `df`, `top`, `free`, `nmon`, `iostat`, `ifconfig`, `crontab`
* Cloudwatch
* Grafana

## Resources
* [20 Command Line Tools to Monitor Linux Performance](https://www.tecmint.com/command-line-tools-to-monitor-linux-performance/)
* [Amazon CloudWatch 지표 사용](https://docs.aws.amazon.com/ko_kr/AmazonCloudWatch/latest/monitoring/working_with_metrics.html)
* [Getting started with Grafana](https://grafana.com/docs/grafana/latest/getting-started/getting-started/)

## Checklist
* 위 Topics의 리눅스 커맨드들은 어떤 커맨드인가요? 운영 중 어떤 상황에 쓸 수 있을까요?
  * lsof :  시스템에 열려 있는 파일을 확인
  * df : 파일시스템, 디스크의 용량 확인
  * top : 시스템의 부하, 스왑영역, cpu, mem 등 종합 적인 상태 확인
  * free : 메모리 현황 확인
  * iostate : 입출력의 상태를 확인
  * ifconfig : 네트워크 인터페이스의 정보를 확인
  * crontab : 주기적으로 실행하는 cron 작업의 정보 확인
  
* Cloudwatch는 어떤 서비스인가요? 우리가 구축한 시스템 관련하여, Cloudwatch에서 제공하는 메트릭들 중 유용한 것은 어떤 것이 있을까요?

  * Cloudwatch는 AWS 서비스의 로그,지표,이벤트 등을 수집하고 모니터링하는 서비스입니다.
  * EC2 CPU 사용량, lambda HTTP 에러 및 동시성 수, ECS CPU 및 MEM 사용량, 클라우드프론트 에러 비율
  
* Grafana는 어떤 역할을 하는 툴인가요? Grafana 외에 비슷한 일을 하는 툴은 무엇이 있을까요?
  * grafana는 시각화 툴입니다. 메트릭으로 제공되는 데이터를 이용하여 운영자가 판단할 수 있는 자료를 시각화합니다.
다른 툴로는 ELK 스택에서 많이 사용하는 키바나가 있습니다. 키바나느 주로 로그의 시각화에서 많이 사용됩니다.

## Quest
* 리눅스 시스템의 모니터링이나 상태 파악을 위한 커맨드를 연습해 보세요.
* Grafana를 통해 지금까지 구축한 전체 시스템에 대한 모니터링 페이지를 구축해 보세요.
* 서버가 비정상 상태일 때, 혹은 서버의 대수에 변화가 있을 때 운영자가 알 수 있도록 슬랙을 통해 Alert을 설정해 보세요.

## Advanced
* 리눅스 시스템을 웹 서버 용도로 사용할 때, 서비스하는 트래픽의 특성에 따라 CPU, 메모리, 파일 I/O 중 어떤 것들이 중요하게 될까요?
  * 이미지나 동영상의 전송이 많다면 데이터를 캐싱할 메모리, 파일을 전송할 시의 I/O 가 중요하다고 생각합니다.
  * 정적 콘텐츠 전송은 작은 파일들을 자주 전송하기 때문에 파일 I/O 가 중요하다고 생각합니다.
  * API 에 대한 요청, 응답을 처리하는 서버는 CPU 가 중요하다고 생각합니다.
