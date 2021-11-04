# Quest 05. 형상관리툴

## Introduction
* git은 2021년 현재 개발 생태계에서 가장 각광받고 있는 버전 관리 시스템입니다. 이번 퀘스트를 통해 git의 기초적인 사용법을 알아볼 예정입니다.

## Topics
* git
  * `git clone`, `git add`, `git commit`, `git push`, `git pull`, `git branch`, `git stash` 명령
  * git 시스템이 프로젝트의 히스토리를 저장하는 방법
  * `.git` 폴더의 내용
* GitHub

## Resources
* [Set up Git](https://try.github.io)
* [깃 브랜칭을 배워봅시다](https://learngitbranching.js.org/?locale=ko)
* [.Git directory](https://githowto.com/git_internals_git_directory)

## Checklist
* 형상관리 시스템은 왜 나오게 되었을까요?
  * 소프트웨어의 개발 유지보수 과정에서 발생하는 변경사항을 체계적으로 관리하기 위해서입니다.
소프트웨어를 개발하는 과정 중 다수의 인원이 작업을 진행하고
고객의 요구사항을 반영하기 위해 코드변경이 빈번하게 발생합니다.
그래서 이를 관리하기 위해 형상관리 시스템이 나오게 되었습니다.
문제가 발생한 지점을 신속하게 발견할 수 있기 때문에 가시성과 추적성이 향상됩니다.
결과적으로 서비스의 품질과 안정성을 높일 수 있습니다.

* git은 어떤 형상관리 시스템이고 어떤 특징을 가지고 있을까요? 분산형 형상관리 시스템이란 무엇일까요? git과 같은 분산형 시스템의 장점은 무엇일까요?
  
  * git은 분산형 형상관리 시스템입니다. 
원격 레포지토리에 코드를 백업한 후 각자의 분산된 시스템에서 작업이 가능합니다.
분산된 시스템에서 작성된 코드들은 원격 레포지토리에 백업하여 관리됩니다.
원격 레포지토리가 동작하지 않더라도 분산된 저장소에 코드가 존재하여 복원이 가능합니다.
분산된 작업환경 구성이 가능하여 다수의 인원이 협업하기 적합합니다.

* git과 GitHub은 어떻게 다를까요?

  * git 은 소프트웨어 버젼 관리를 하기 위한 오픈 소스 소프트웨어입니다.
  * github 는 git 으로 관리되는 코드를 저장할 수 있는 git 레포지토리를 제공하는 서비스를 말합니다.
  
* git의 clone/add/commit/push/pull/branch/stash 명령은 무엇이며 어떨 때 이용하나요? 그리고 어떻게 사용하나요?

  * clone : 원격 레포지토리에 저장소를 복제해 오는 명령입니다.
    * ex ) git clone https://github.com/[USERNAME]/[REPOSITORY_NAME].git
    
  * add : 작업디렉토리에서의 변경 내용을 스테이징 영역에 추가할 때 사용합니다.
    * ex ) git add [디렉토리 | 파일명]
    
  * commit : git add 명령을 통해 스테이징 영역에 저장된 내용을 하나의 의미있는 변경분으로 생성합니다.
    * ex ) git commit -m "커밋메세지"
    
  * push : 로컬저장소에 저장된 커밋들을 원격 레포지토리의 특정 브랜치에 적용합니다.
    * ex ) git push [원격레포지토리명] [브랜치명]
    
  * pull : 원격레포지토리에서 새로 적용된 commit 을 로컬 저장소로 가져와서 적용합니다.
    * ex ) git pull [원격레포지토리명] [브랜치명]
    
  * branch : 브랜치를 신규로 생성합니다.
    * ex ) git branch [브랜치명]
    
  * stash : 마무리하지 않은 작업들을 임시로 저장하고 나중에 다시 작업할 수 있도록합니다.
    * ex ) git stash
    
* git의 Object, Commit, Head, Branch, Tag는 어떤 개념일까요? git 시스템은 프로젝트의 히스토리를 어떻게 저장할까요?

  * Object
  
  * Commit
  
  * Head
  
  * Branch
  
  * Tag
  
  
* 리모트 git 저장소에 원하지 않는 파일이 올라갔을 때 이를 되돌리려면 어떻게 해야 할까요?

  *
  
## Quest
* GitHub의 개인 계정에 이번 퀘스트를 위한 리포를 만들어 보세요.
* Quest 04에서 vi로 입력한 웹 서비스 대신 GitHub의 저장소를 clone하여 같은 일을 하는 서버를 띄워 보세요.
* 리포지토리에 민감한 정보(개인정보, 패스워드 등)가 들어가지 않도록 주의합니다.

## Advanced
* Mercurial은 어떤 형상관리 시스템일까요? 어떤 장점이 있을까요?
* 실리콘밸리의 테크 대기업들은 어떤 형상관리 시스템을 쓰고 있을까요?
