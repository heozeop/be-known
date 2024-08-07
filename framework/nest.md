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
