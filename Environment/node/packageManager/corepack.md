# corepack
[ref](https://nodejs.org/api/corepack.html#supported-package-managers)
package manager를 시스템에 맞게 대신 설치해 주는 NodeJS의 툴

## 동작 과정

1. corepack enable: (22버전 기준)실험 기능이기 때문에 명시적인 enable이 필요
1. package 찾기
    1. package.json에 명시된 packageManager 참조
    1. corepack use 명령어로 명시된 packageManager 참조
1. 덮어쓰기: `corepack install --global (yarn/pnpm)@version`

## 적용 패키지
pnpm, yarn

### npm은 어찌 된 거냐
- corepack으로 설치는 할 수는 있으나 [shim](https://en.wikipedia.org/wiki/Shim_(computing))이 기본적으로 enabled 되어 있지는 않다.
    1. corepack이 intercept할 수 없어서 npm이 프로젝트 세팅과 무관하게 돌 수 있다.
    2. global npm이 돌 수 있다.
