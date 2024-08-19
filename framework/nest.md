# NestJS
## Philosophy
어플리케이션 아키텍처를 제공해 줌으로써, 개인/팀이 테스트/스케일/낮은 응집도를 가진 앱을 만들 수 있도록 하는 것

## Overview
### Controller
들어오는 요청의 처리 및 응답을 담당

#### Decorator
- Controller
    - 컨트롤러 선언을 위해 사용하는 클래스 데코레이터
    - route prefix를 설정 가능
    - host 설정을 바탕으로 [subdomain routing](https://docs.nestjs.com/controllers#request-object)도 가능함
        - express only
    - 
- Get/Post/Put/Patch/Delete/Options/Head/All
    - HTTP method 데코레이터
    - route에 whildcard 설정 가능
- HttpCode
    - 응답 코드 지정
- Header
    - 응답 헤더 지정
- [Redirection](https://docs.nestjs.com/controllers#request-object)
    - redirection 해줌
    - return value가 설정을 override 함.
- Req/Res
    - 라이브러리 단의 요청/응답 객체를 가져오는 데코레이터
    - [request 관련 데코레이터들](https://docs.nestjs.com/controllers#request-object)
    - Res 쓸때는 라이브러리의 타입을 가지고 있어야 함.


#### BestPractice
##### 응답 처리 방식
1. Standard
    - 응답 주면 NestJS가 알아서 직렬화
    - HttpCode 지정
2. Library-specific
    - express등의 응답 객체를 직접 사용하는 방법
    - header만 지정하는 경우 등 1번 방식을 함께 사용하고 싶으면 `@Res({passthrough: true})`와 같이 처리 해야 함.]
        - [ref](https://docs.nestjs.com/controllers#request-object)

### Provider
module애서 Provider로 정의된 plain Javascript Class를 의미한다.


#### Decorator
- Injectable
    - class가 Nest IoC 컨테이너에 의해 처리될 수 있음을 마크함.
    - ```typescript
      @Controller('something')
      export class SomethingController {
        constructor(private readonly somethingService: SomethingService) {}
      }
      ```

#### BestPractice
##### 참조시 private readonly 사용하기
- private: 내부에서만 참조한다는 것을 명시(외부로 드러나지 않음)
- readonly: reference 변경을 참조 내부에서 하지 않음을 명시함.

#### 개념들
##### Custom Provider
- [ref](https://docs.nestjs.com/fundamentals/custom-providers)
- Inversion of Control(IoC)를 하는 방법이 존재함.

##### Optional Provider
- ```typescript
    @Injectable()
    export class HttpService<T> {
    constructor(@Optional() @Inject('HTTP_OPTIONS') private httpClient: T) {}
    }
  ```
- 그냥 기본값 사용해도 되는 상황인 경우

##### Property base injection
- constructor에서 하는게 아니라 property에 decorator 붙여서 처리하기

### Module
`Module` decorator가 붙은 클래스

#### Decorator
- Module
    - Nest가 application architecture를 구성하는데 필요한 정보를 줌

#### 개념
##### Feature Module
- export된 provider를 module import를 통해 받는 방법

##### shared modules
1. 기본적으로 singleton이라 돌려씀

##### module re-exporting
- module을 export해서 module에서 선언된 exports들 참조가능

##### Dependency Injection
- 기본적으로는 모듈 호출될 때 됨
- circular dependency 존재하면 터짐

##### global module
- Global 데코레이터 이용해서 module을 global scope로 등록
- 1번만 등록 되어야 함. 보통 root에서 해줌.

#### Dynamic module
- [ref](https://docs.nestjs.com/fundamentals/dynamic-modules)
- module 선언을 다이나믹(?)하게 할 수 있도록 만듦

### Middleware
route handler 앞단에서 request/response 처리하는 함수
- 기본적으로는 express의 것과 동일
    - code 수행
    - request/response 처리
    - 다음 middleware 호출

#### 적용 방법
- [ref](https://docs.nestjs.com/fundamentals/dynamic-modules) / 참조 필수!
- NestMiddleware interface 구현
- @Injectable 데코레이터 추가 해야 함.
- DI 가능
- route에 사용할 수 있는 [wildcard 규칙](https://docs.nestjs.com/middleware#route-wildcards)

#### [MiddlewareConsumer](https://docs.nestjs.com/middleware#middleware-consumer)
- fluent style로 작업을 할 수 있는 helper 클래스
- apply하면 한개/여러개 등록 가능
- forRoute에는 한개/여러개/RouteInfo 클래스/controller 클래스 넣을 수 있음
- exclude하면 path, method 제외 가능

#### [functional middleware](https://docs.nestjs.com/middleware#functional-middleware)
- 단순한거는 middleware function으로 설정 가능
- apply로 추가 가능

#### [global middleware](https://docs.nestjs.com/middleware#global-middleware)
- nest app create할 때, use에 추가해주면 됨.

### ExceptionFilter
unhandled exception 다뤄주는 layer
- http-errors 라이브러리를 일부 지원함
    - statusCode와 message가지고 있는 Object 던지면 잘 잡아줌
#### HttpException
- nest에서 만든 익셉션
- option에 cause로 error 넘기면 응답으로는 안나가고 로깅만 해줌 -> message만 나감

#### Exception Filters
- @Catch로 마킹, ExceptionFilter implement해서 선언
- 응답 변형이 가능한데, 이때 fastify는 응답 하는 함수가 다른 것 유의
- @UseFilters로 binding 가능
    - 이때 instance로 생성해서 넘기는 것도 가능한데, 메모리 관점에서 낭비가 있을 수 있으니 DI하는 것 고려 필요
- useGlobalFilters
    - gateway나 hybrid application에서는 동작 안함
    - DI도 안됨, 외부 맥락으로 주입 됨.
        - DI 하고 싶으면 `APP_FILTER`라는 provider로 `AppModul`에서 주입할 필요가 있음

### Pipe
`PipeTransform<T,R>` interface를 구현하는 @Injectable 클래스
#### 일반적인 usecase
1. transformation
1. validation

#### 동작
메소드 호출 직전에 끼어들어서 pipe 동작을 수행
이때 대상이 되는 method는 controller route handler다.

- pipe에서 터지면 exception filter가 잡을 수 있다.
- [built in pipes](https://docs.nestjs.com/pipes#built-in-pipes)

#### transform 함수
- PipeTransform 구현체가 구현해야만 하는 메소드
- 파라미터는 value와 metadata 2개
    - value는 현재 넘겨진 argument
    - [metadata는 아래와 같은 타입](https://docs.nestjs.com/pipes#custom-pipes)
        ```typescript
        export interface ArgumentMetadata {
            type: 'body' | 'query' | 'param' | 'custom';
            metatype?: Type<unknown>;
            data?: string;
        }
        ```
        - js에서는 object 타입일 것임

#### 스키마 베이스 validation
- 모든 타입을 다루는 generic middleware는 불가함
    - middleware는 execution context를 모르기 때문
    - 이게 의도됨
- 방안 
    1. [Object Schema Validation](https://docs.nestjs.com/pipes#object-schema-validation)
        - zod 등 validator 이용하는 방식
    1. [Class validator](https://docs.nestjs.com/pipes#class-validator)
        - class-validator, class-transformer 이용하는 방식
- [global pipe](https://docs.nestjs.com/pipes#global-scoped-pipes)
    - DI 불가, context 밖에서 등록 됨
    - DI하려면 `APP_PIPE`로 등록해야함.

### Guard
CanActivate interface를 구현하는 @injectable 클래스
Authorization, Authentication에만 관심 있음

#### middleware보다 나은점
- execution context를 알고 있다.
    - 다음에 뭐가 호출되는지 알 수 있다.

#### CanActivate
- ExecutionContext라는 하나의 인스턴스를 인자로 받음

### Interceptor
NestInterceptor 인터페이스를 구현하는 @Injectable 클래스
모든 interceptor는 intercept 함수를 구현함.

#### basic
- ExecutionContext (1번 인자)
- CallHandler (2번자인자)
    - handle 메소드 구현하는 인터페이스
    - next로 보통 사용하며, handle 메소드는 observable 리턴함.

#### 활용 케이스
1. Logger
1. Aspect Interception

### Custom Route Decorators
#### Param Decorator
- [ref](https://docs.nestjs.com/custom-decorators#param-decorators)
- user decorator
    ```typescript
    import { createParamDecorator, ExecutionContext } from '@nestjs/common';

    export const User = createParamDecorator(
        (data: unknown, ctx: ExecutionContext) => {
            const request = ctx.switchToHttp().getRequest();
            return request.user;
        },
    );
    ```

#### Working with pipes
- [ref](https://docs.nestjs.com/custom-decorators#working-with-pipes)
- decorator를 사용할 때 그냥 validator 넣을 수도 있음

#### Decorator composition
- [ref](https://docs.nestjs.com/custom-decorators#decorator-composition)
- `applyDecorators`를 이용해서 여러개의 decorator를 한번에 적용
