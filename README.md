<p align="center">
    <img src="https://github-production-user-asset-6210df.s3.amazonaws.com/108314208/342624327-98bd0fd8-fa9e-40ed-897a-9ac47a75d224.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAVCODYLSA53PQK4ZA%2F20240625%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20240625T073047Z&X-Amz-Expires=300&X-Amz-Signature=058812aa7cc23d3bf80f3b9da1590a4006ff63a2467fb2e3b70367b36e70354e&X-Amz-SignedHeaders=host&actor_id=108314208&key_id=0&repo_id=819778043" alt="Nest Logo" />
</p>

## Description

`describe()`
* test suite 를 작성하는 블록
* test suite 란 테스트들을 의미있는 단위로 묶은 것
* test suite 를 모아서 더 큰 단위의 test suite 만들 수 있음
* test suite 는 테스트 수행에 필요한 환경 설정, 공통 모듈 생성 등과 같이 세부 test case 가 구행되기 위한 기반을 마련함

`it()`
* 특정 테스트 시나리오 작성
* 각 it() 구문은 별개의 test case 로 다뤄져야 하며, 서로 의존관계가 없어야 함




test case 작성법은 TDD 혹은 BDD (Behavior-Driven Development) 스타일로 할 수 있는데 <br>
여기선 Given / When / Then BDD 스타일로 테스트 코드를 작성해본다.

* **Given**
  * 해당 test case 가 동작하기 위해 갖춰져야 하는 선행 조건 (=어떤 상황이 주어졌을 때)
* **When**
  * 테스트하고자 하는 대상 코드 실행 (=대상 코드가 동작한다면)
* **Then**
  * 대상 코드의 수행 결과 판단 (=기대한 값과 수행 결과가 맞는지)

`describe()` 의 첫 번째 인수는 문자열로 test suite 와 test case 의 이름이고,<br>
두 번째 인수는 수행된 코드가 포함된 콜백 함수이다.

```typescript
describe('UserHandler', () => {
    const userService: UserService = new UserService();
    
    describe('create', () => {
        it('should create user', () => {
            // Given
            // ...
            // When
            // ...
            // Then
            // ...
        });

        it('should throw error when user already exists', () => {
          // Given
          // ...
          // When
          // ...
          // Then
          // ...
        });
    });
});
```
`describe()` 와 `it()` 외에 `Setup` 과 `TearDown` 개념이 있다.

* `SetUp`
    * test suite 내에서 모든 test case 를 수행하기 전에 수행되어야 하는 선행 조건 실행 (=반복 작업 줄임)
* `TearDown`
  * 테스트 후 후처리 공통 처리

---

#### Jest 는 아래 4가지 구문을 제공한다.

* `beforeAll()`
  * test suite 내의 모든 test case 수행 전 한번만 실행
* `beforeEach()`
  * 각 test case 가 수행되기 전마다 수행
* `afterAll()`
  * 모든 test case 가 수행된 후 한번만 실행
* `afterEach()`
  * 각 테스트가 수행된 후마다 수행

---

위에 잠깐 테스트 프레임워크의 구성 요소를 설명하면서 **Test Double** 에 대해 언급했다.<br>
Test Double 은 외부 모듈을 임의의 객체로 다루는 것으로 Dummy, Fake, Stub, Spy, Mock 으로 나뉜다.

* `Dummy`
  * 테스트를 위해 생성된 가짜 데이터
  * 일반적으로 매개변수 목록을 채우는 데에만 사용됨

* `Fake`
  * DB 에 있는 데이터를 테스트한다고 할 때 실제 DB 사용 시 I/O 에 많은 비용과 시간이 소요되므로 인메모리 DB 와 같이 메모리에 데이터를 적재해서 속도 개선
  * prod 환경에서는 테스트 수행 도중 시스템이 비정상 종료되면 잘못된 데이터가 남게 되므로, 잘못된 데이터가 남아도 상관없는 세션 등과 같은 것을 대상으로 테스트할 때 사용

* `Spy`
  * 테스트 수행 정보 기록
  * 테스트 도중 함수 호출에 대해 해당 함수로 전달된 매개변수, 리턴값, 예외, 함수를 몇 번 호출했는지와 같은 정보 기록

* `Stub`
  * 함수 호출 결과를 미리 준비한 응답으로 제공

* `Mock`
  * Stub 과 비슷한 역할
    * 테스트 대상이 의존하는 대상의 **행위에 대해 검증이 필요하면** `Mock` **사용, 상태에 대해 검증이 필요하면 `Stub` 사용**
