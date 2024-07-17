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

## Expression
### literal
- boolean: true / false
- null: null
- number: JSON이 지원하는 number 타입
- string: ''로 감싸지거나 그냥 쓰여진 string
    - ""로 감싸면 터짐
### falsy value
- `false, 0, -0, "", '', null`) => false
### operator
- [ref](https://docs.github.com/en/actions/learn-github-actions/expressions#operators)
- 일반 비교/논리 연산자 생각하면 됨
- 비교 연산 시 string의 case는 무시함.
- 숫자 연산에서 string 바꿀때 [fromJSON](https://docs.github.com/en/actions/learn-github-actions/expressions#fromjson) 함수 사용할 수 있음
- NaN은 항상 true
### Functions
- [ref](https://docs.github.com/en/actions/learn-github-actions/expressions#functions)
1. [contains](https://docs.github.com/en/actions/learn-github-actions/expressions#functions)
    - `constains(search, item)`
        - true: `search`에 `item`있는 경우
            - `search`가 array면 `item`은 element, string이면 substring
        - false: true가 아닐 경우
1. [startsWith](https://docs.github.com/en/actions/learn-github-actions/expressions#startswith)
1. [endsWith](https://docs.github.com/en/actions/learn-github-actions/expressions#endswith)
1. [format](https://docs.github.com/en/actions/learn-github-actions/expressions#format
    - `{index}` => 데이터 치환
1. [join](https://docs.github.com/en/actions/learn-github-actions/expressions#format)
    - `join(array, optionalSeperator)`, optionalSeperator는 기본값 `,`을 가짐
1. [toJSON](https://docs.github.com/en/actions/learn-github-actions/expressions#format)
1. [fromJSON](https://docs.github.com/en/actions/learn-github-actions/expressions#format)
1. [hashFiles](https://docs.github.com/en/actions/learn-github-actions/expressions#format)
    - path 패턴에 맞는 파일의 hash 패턴을 짜냄, SHA-256 해시임.
    - ,를 이용해서 여러개 hash pattern 설정 가능
### Status check functions
- [ref](https://docs.github.com/en/actions/learn-github-actions/expressions#status-check-functions)
1. [success](https://docs.github.com/en/actions/learn-github-actions/expressions#success)
    - 이전 step이 모두 성공한 경우 true
1. [always](https://docs.github.com/en/actions/learn-github-actions/expressions#always)
    - 항상 true
1. [cancelled](https://docs.github.com/en/actions/learn-github-actions/expressions#cancelled)
    - workflow가 cancel된 경우 true
1. [failure](https://docs.github.com/en/actions/learn-github-actions/expressions#failure)
    - 이전 step/job 중 하나라도 실패한 경우 true
### Object Filter
- [ref](https://docs.github.com/en/actions/learn-github-actions/expressions#failure)
- `*` 통해서 object destruct 가능


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
