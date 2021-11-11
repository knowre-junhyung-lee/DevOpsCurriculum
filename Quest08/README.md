# Quest 08. 배포 자동화 하기

## Introduction
* 이번 퀘스트에서는 여러 대의 서버에 자동 배포를 구현하는 방법에 대해 알아보겠습니다.

## Topics
* Systems Manager
* Fargate
* Blue/Green Deployment

## Resources
* [Systems manager](https://aws.amazon.com/ko/systems-manager/)
* [AWS Fargate](https://aws.amazon.com/ko/fargate)
* [Blue-Green Deployment](https://www.redhat.com/ko/topics/devops/what-is-blue-green-deployment)

## Checklist
* AWS의 Systems Manager는 어떤 서비스인가요?

  * AWS Systems manager 는 EC2 또는 RDS 의 운영을 자동화할 수 있는 사용자 인터페이스입니다.
리소스의 제어와 운영에 필요한 각종 데이터를 통합관리할 수 있습니다.

* AWS의 Fargate는 어떤 서비스인가요? 어떤 장점을 가지고 있나요?
  
  * 컨테이너 환경을 제공하는 서버리스 컴퓨팅의 한 종류입니다.
기존에는 ECS 에서만 서비스가 제공되었지만 현재는 쿠버네티스 환경의 워커 노드역할을 서버리스로 사용할 수 있습니다.
관리형 서비스로서 패치, 보안, 리소스 조정 등의 운영 부담을 줄일 수 있습니다.
  
* Blue/Green Deployment라는 것은 어떤 개념일까요?

  * 블루 그린 배포는 새로운 버젼의 어플리케이션을 배포할 때 기존과 동일한 환경을 하나 더 구성하는 방법입니다.
기존의 버젼과 환경이 블루, 새로운 버젼과 환경이 그린입니다.
새 버젼 배포간에 블루는 롤백을 대비하여 그대로 유지한 후에 그린을 생성합니다.
생성된 그린을 통해 서비스 트래픽이 완전히 옮겨지도록 합니다.
이후 서비스를 모니터링하면서 문제가 발생하지 않는다면 새로운 버젼으로 서비스를 제공하고
구버젼의 환경을 제거하는 방식입니다.

## Quest
* AWS의 Systems Manager를 이용하여, 로컬 CLI 컨테이너 이미지를 배포하고 리모트 서버에서 그 이미지를 교체하여 띄울 수 있게 해 보세요. 쉘 스크립트 한 개로 이 모든 것이 이루어질 수 있게 하면 가장 좋습니다!
* 이번에는 EC2 대신 Fargate를 이용하여 같은 서비스를 구현해 보세요. 수동으로 배포하려면 어떻게 해야 할까요?
* Fargate에도 처음에 EC2에 한 배포 자동화를 구현해 보세요. 이 역시 쉘 스크립트 한 개로 이 모든 것이 이루어질 수 있게 하면 가장 좋습니다!

## Advanced
* 컨테이너 오케스트레이션이란 무엇일까요? 이를 달성하기 위한 방법으로 Fargate 외에 어떤 수단들이 있을까요?
  * 컨테이너 오케스트레이션이란 컨테이너의 배포, 로드밸런싱, 가용성, 스케일링 등의 관리를 수월하게 해주는 툴입니다. 대표적으로는 구글에서 개발한 쿠버네티스나 도커 스웜 등이 있습니다. 
