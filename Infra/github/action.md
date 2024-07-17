학습 자료
- [MS learn](https://learn.microsoft.com/en-us/collections/n5p4a5z7keznp5)
- [Github Docs](https://docs.github.com/en/actions)

# Github Action
소프트웨어 배포 작업을 자동화하는 packaged script

## 찾을 때는
1. open source
    1. 이해하고 쓰라고 권장
1. market place

## 타입
- Container action, Javascript action, Composite actions

## 구성 요소
### workflow
- Github 프로젝트를 빌드, 테스트, 패키징, 릴리즈, 배포하는 자동화된 프로세스
#### on
- [trigger](https://docs.github.com/actions/using-workflows/events-that-trigger-workflows)
1. schedule
    - [POSIX cron syntax](https://pubs.opengroup.org/onlinepubs/9699919799/utilities/crontab.html#tag_20_25_07) 따라서 설정 가능
1. workflow_dispatch
    - Github REST API 혹은 Action tab의 Run workflow 버튼 누른 경우 실행
    - 실행 브랜치, 입력 등 선정 가능
1. repository_dispatch
    - Github API로 실행하는 웹훅 이벤트
    - POST: /repos/{owner}/{repo}/dispatches + webhook event
1. check_run
    - 웹훅 트리거

#### runs-on
- specify runner: [container / machine] in [self-hosted / github-hosted]

### Job
- 워크플로우가 가지는 하나 이상의 동작 흐름

### Step
- job에 속하는 작업 단위

### Action
- 실행되는 단일 커맨드

## 문법
### conditional keyword
- `if ${{ expression }}`
- 자동으로 expression으로 처리해주는게 있긴함.

## trigger
### watch
- [ref](https://docs.github.com/en/actions/using-workflows/events-that-trigger-workflows#watch)
- star 달리면 trigger
### workflow_call
- [ref](https://docs.github.com/en/actions/using-workflows/events-that-trigger-workflows#workflow_call)
- 워크 플로우를 동작하게 호출 할 수 있음.
### workflow_dispatch
- [ref](https://docs.github.com/en/actions/using-workflows/events-that-trigger-workflows#workflow_dispatch)
- 직접 trigger하는 방식
    - default branch를 기준으로 workflow 동작함.
- `inputs` 과 `ref`를 넘길 수 있음
    - `inputs`는 10개 까지 가능 (옵션은 더 쓸 수 있는 것으로 보임)
    - `inputs`의 최대 payload size는 65,535(2^16)
### workflow_run
- [ref](https://docs.github.com/en/actions/using-workflows/events-that-trigger-workflows#workflow_run)
- 3개의 호출 방식 상태가 존재
    - completed / requested / in_progress
- default branch를 기준으로 동작함
- 최대 3개 chain만 가능함.

## 효율적인 도구
### actions/checkout
- [ref](https://github.com/actions/checkout)
- 현재(24.07.17) 기준 
