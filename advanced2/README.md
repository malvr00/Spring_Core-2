# 로그 추적기 - 쓰레드 로컬 사용하여 구현
use: java 17, spring boot 3.2.5, spring web, lombok<br/>

### 로그 추적기 구현체 { 필드사용, ThreadLocal }
이전 버전에서는 `TraceId`가 중복되는 문제가 있었다. `TraceId`를 필드사용해서 처리하는 과정과 ThreadLocal을 사용해 처리하는 과정의 프로잭트다.
- 먼저 `TraceId`를 필드에 주입 받아서 재사용한다,
  - 이럴 경우 동시에 요청이 들어왔을 경우 동시성 문제가 발생한다.
- ThreadLocal을 활용한 `TraceId` 처리
  - `TraceId`를 ThreadLocal로 바꿔서 중복문제를 해결했다.
  - ThreadLocal을 사용하면 각 쓰레드마다 전용 보관장소를 제공해주고, 그 때문에 두 개 이상의 요청이 들어오더라도 `TraceId`가 중복되는 문제를 해결할 수있다
  - ThreadLocal을 사용할 경우 사용이 완료되면 꼭 `TreadLocal.remove()`를 통해 꼭 정리해줘야한다. 그렇지 않으면 또 다른 문제가 발생한다.