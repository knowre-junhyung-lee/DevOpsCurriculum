# Quest 14. 코드로 인프라 관리하기

## Introduction
* 이번 퀘스트에서는 인프라를 코드로 관리하는 법에 대해 알아보겠습니다.

## Topics
* IaC
* Terraform
  * State
  * Import
  * AWS Provider

## Resources
* [Infrastructure as Code](https://en.wikipedia.org/wiki/Infrastructure_as_code)
* [Terraform](https://www.terraform.io/intro/index.html)
* [Introducing Terraform](https://www.44bits.io/ko/post/terraform_introduction_infrastrucute_as_code)
* [Terraform state](https://www.terraform.io/docs/state/index.html)
* [Terraform Provider](https://registry.terraform.io/providers/hashicorp/aws/latest/docs)

## Checklist
* IaC(Infra as Code)는 어떤 개념인가요? 이러한 개념이 왜 생기게 되었을까요?
  * IaC 란 인프라를 코드로 정의하는 기술입니다.
인프라를 구축하는 과정은 반복되는 일이 많았고 자동화를 위해서 스크립트를 작성하는 것이 일반적이었습니다.
하지만 스크립트를 통한 자동화는 불편하고 불변성을 유지하기 힘들었습니다.
요즘 새로 개발된 IaC tool 들은 인프라의 상태를 가지고 있으며 항상 코드를 통해서 동일한 프로비저닝이 가능합니다.
이러한 장점을 통해 인프라의 일관성을 유지할 수 있고 구성 변경을 추적할 수 있는 장점이 있습니다.
또한 인프라가 코드로서 관리되기 때문에 버젼 관리가 가능하다는 장점도 있습니다.

* 테라폼은 어떤 소프트웨어인가요? 다른 IaC와 비교하여 어떤 장점을 가지고 있을까요?

  * 테라폼은 하시코프 사에서 개발한 클라우드 IaC 도구 입니다.
여러 클라우드 벤더사의 인프라를 프로비저닝할 수 있습니다.
해당 벤더사에서 제공하는 API를 테라폼을 통해서 이용할 수 있도록 개발되었습니다.
벤더 중립적인 도구이기 때문에 벤더사에 lock-in 하지 않는 장점이 있습니다.
  
* 테라폼의 State는 무엇일까요? 기존에 AWS 콘솔을 통해 정의된 리소스를 테라폼의 State에 가져오려면 어떻게 해야 할까요?

  * 테라폼의 State 는 테라폼을 통해서 선언한 인프라의 상태를 가지고 있는 파일입니다.
기존에 정의된 인프라를 테라폼에 가져오기 위해서는 import 명령어를 사용하면됩니다.
공식 문서를 통해서 import 가능한 리소스인지를 확인하고 작성법을 참조하여 진행합니다.
먼저 해당하는 리소스의 tf 파일을 작성하고 해당하는 리소스 작성법으로 import 명령어를 실행합니다.


## Quest
* 지금까지 구축했던 다음의 인프라를 모두 삭제하고 테라폼 코드로 재구축해 보세요.
  * VPC
  * Fargate 기반의 API 서비스
  * 람다 기반의 서비스
  * S3와 Cloudfront 기반의 정적 웹사이트

## Advanced
* 테라폼 외의 IaC 툴에는 어떤 것이 있을까요? 테라폼에 비해 어떤 장점들을 가지고 있을까요?
  * aws의 클라우드 포메이션, 구성 관리에 사용되는 앤서블 등이 있습니다.
클라우드 포메이션은 AWS 에서만 사용이 가능하고 최신의 AWS 리소스 프로비저님 기능이 빠르게 제공됩니다.
앤서블은 구성관리에 많이 사용되는 도구입니다. EC2 와 같은 Iaas 서비스를 사용할 때에는 
해당 인프라가 처음 프로비저님하는 시점에 user_data 를 통해 설정이 가능합니다.
하지만 앤서블은 ssh 를 통해서 구성 관리를 지속적으로 진행할 수 있습니다.
