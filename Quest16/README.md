# Quest 16. 배포 파이프라인

## Introduction
* 이번 퀘스트에서는 CI/CD 파이프라인이 왜 필요한지, 어떻게 구축할 수 있는지 등에 대해 다룹니다.

## Topics
* Continuous Integration
* Continuous Delivery
* AWS Codebuild

## Resources
* [Continuous Integration](https://aws.amazon.com/ko/devops/continuous-integration/)
* [Continuous Delivery](https://aws.amazon.com/ko/devops/continuous-delivery/)
* [AWS Codebuild](https://aws.amazon.com/ko/codebuild/getting-started/)

## Checklist
* CI/CD는 무엇일까요? CI/CD 시스템을 구축하면 어떤 장점이 있을까요?
  * CI 는 지속적으로 코드를 통합하는 것 입니다. 코드의 새로운 변경 사항이 빌드 및 테스트되어 레포지토리에 통합될 수 있게 하는 것입니다.
  * CD 는 지속적인 코드를 배포하는 것 입니다. 개발, 스테이징, 프로덕션 등의 환경에 코드 변경 사항이 릴리즈되도록 하는 것 입니다.
  
* CI 시스템인 Travis CI, Jenkins, Circle CI, Github Actions, AWS Codebuild 의 차이점과 장단점은 무엇일까요?
  * Travis CI : 깃허브와 최적화된 연결이 가능합니다. 설치가 필요없는 웹서비스입니다.
  * Jenkins : 자바로 작성된 오픈소스입니다. 직접 서버를 설치해서 운영합니다. 플러그인이 다양합니다.
  * Circle CI : 여러 플랫폼과의 연동이 용이합니다.서비스 형태로 제공됩니다.작업의 병렬처리가 가능합니다.
  * Github Actions : 깃허브와 통합되어 있습니다. 여러 운영체제, 런타임에서 테스트가 가능합니다.
  * AWS Codebuild : AWS의 다른 서비스와 연동하기 용이합니다. 관리형 서비스입니다.

## Quest
* AWS Codebuild를 이용하여, 특정 브랜치에 푸시를 하면 테스트를 한 뒤 모노리포에 있는 모든 패키지가 한 번에 배포되는 시스템을 만들어 보세요.
* 이 시스템의 CI/CD를 더 효율적으로 할 수 있는 아이디어에는 어떤 것들이 있을까요? 다섯 가지 이상의 아이디어를 제시해 보세요.
  * 각 패키지 별로 별도록 배포가 가능하도록 구성합니다.
  * 코드에 대한 테스트를 자동화합니다.
  * 빌드에 대한 결과를 자동으로 알리도록 구성합니다.
  * 빌드 테스트 간 사용하는 모듈을 캐싱합니다. 
  * 빌드 런타임을 효율화합니다. (빌드 실행환경의 커스텀이 가능하다면)
  * 롤백에 대한 자동화

## Advanced
* 빅테크 회사들이 코드를 빌드하고 배포하는 시스템은 어떻게 설계되고 운영되고 있을까요?
  * 넷플릭스를 예로 들면, 젠킨스, 젠킨스 X, 일렉트릭 클라우드를 사용한다고 합니다.
넷플릭스는 인프라 환경을 AWS 로 전부 이동하였고 msa 아키텍쳐 기반의 ci/cd 를 구축하여 하루에 100번 이상의 릴리즈를 진행한다고 합니다.
