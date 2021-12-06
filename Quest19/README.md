# Quest 19. 스트레스 테스트

## Introduction
* 이번 퀘스트에서는 스트레스 테스트와 오토 스케일링에 대해 알아보겠습니다.

## Topics
* Stress Test
* Artillery
* AWS Auto Scaling
* Fargate Auto Scaling
* Lambda Concurrency

## Resources
* [Stress testing tutorial](https://www.guru99.com/stress-testing-tutorial.html)
* [Artillery](https://artillery.io/)
* [AWS AutoScaling](https://aws.amazon.com/ko/about-aws/whats-new/2018/01/introducing-aws-auto-scaling/)
* [Auto Scaling](https://aws.amazon.com/ko/blogs/korea/category/compute/auto-scaling/)
* [ECS Auto Scaling](https://docs.aws.amazon.com/ko_kr/AmazonECS/latest/developerguide/service-auto-scaling.html)
* [Lambda Concurrency](https://docs.aws.amazon.com/lambda/latest/dg/configuration-concurrency.html)

## Checklist
* 스트레스 테스트는 왜 하는 것일까요?
  * 첫번째, 시스템의 한계점을 미리 테스트하여 최대 성능을 예측할 수 있습니다.
  * 두번째, 해당 시스템이 설계 시 의도한 사용량을 층족하는지 확인할 수 있습니다.
  * 세번째, 문제가 발생했을 시의 동작을 예측할 수 있습니다.
  
* 스트레스 테스트의 진행에는 어떤 방법론들이 있을까요?
  * Distributed Stress Testing: 스트레스 서버에서 테스트 할 시스템을 클라이언트로 등록하여 중앙에서 관리하며 테스트합니다.
  * Application Stress Testing: 어플리케이션의 데이터, 락킹, 네트워크 병목 현상 등의 결함을 찾는 테스트입니다.
  * Transactional Stress Testing: 두개 이상의 어플리케이션 간 트랜잭션의 스트레스 테스트입니다.
  * Systemic Stress Testing: 여러 시스템에 걸쳐 테스트 하는 통합 테스트입니다.
  * Exploratory Stress Testing: 비정상적인 상황들을 시나리오로 만들어 테스트합니다.

* AWS의 Auto Scaling은 어떤 서비스일까요? Fargate에서는 어떻게 적용할 수 있을까  
  * AWS의 Auto Scaling은 시스템의 CPU, MEM 등 의 사용량이 일정 조건을 만족하면, 시스템을 수평적으로 증설해주는 서비스입니다. Fargate	의 서비스에 연결한 ELB 와 연동하여 사용량에 따라 태스크를 조절할 수 있도록 설정합니다.

* Lambda의 동시 실행은 어떠한 개념일까요? 부하가 많은 서비스에서 이 지표를 어떻게 모니터링 해야 할까요?
  * Lambda의 동시 실행은 Lambda 함수가 동시에 실행될 수 있게 하는 개념입니다.
동시 실행은 리전별 1000개로 정의되어 있습니다. 해당 동시성이 모두 소진되면 서비스에 문제가 발생할 수 있습니다.
Lambda 함수의 Timeout, HTTP 에러, 동시성 수에 대한 임계치를 설정하여 운영자에게 알림을 보낼 수 있도록 구성해야합니다.

## Quest
* 우리의 컨테이너 기반 서버를 일부러 약간 무겁게 만들어 봅시다. 일부러 서버의 부하를 주려면 어떤 방법이 있을까요?
* Artillery를 이용하여 스트레스 테스트 시나리오를 작성하고, 부하를 가해 보세요.
* Fargate의 Auto Scaling 기능을 설정하여, 초당 일정 이상의 부하가 걸리면 자동으로 컨테이너를 늘리고, 부하가 줄면 자동으로 컨테이너의 수를 줄이게 만들어 보세요.

## Advanced
* 실제 세상에서 자주 업데이트 되는 서비스가 있다고 할 때, 이런 서비스를 스트레스 테스트 하는 데에는 어떤 전략들이 있을까요? 각각의 전략들은 어떤 상황에서 사용될 수 있을까요?
  * 실제 서비스 환경에서는 테스트하기 어렵기 때문에 최대한 동일한 환경을 구성하여 사전에 테스트하는 방법입니다.
스테이징 환경에서 QA 를 진행함과 동시에 업데이트된 부분에 스트레스 테스트를 진행합니다.
스테이징 환경에서 문제가 없더라도 서비스 환경에서는 문제가 발생할 수 있기 때문에 롤백 방안을 마련합니다.
스트레스 테스트를 자동화하여 비용을 절감하고 휴먼에러를 방지합니다.
