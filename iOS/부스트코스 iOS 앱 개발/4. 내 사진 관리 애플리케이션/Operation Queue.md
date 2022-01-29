# Operation Queue

Operation은 태스크와 관련된 코드와 데이터를 나타내는 추상 클래스이다. Operation Queue는 연산(Operation)의 실행을 관리한다. 대기열(Queue)에 추가한 동작은 직접 제거할 수 없다. 연산은 작업이 끝날 때까지 대기열에 남아 있다. 연산을 대기열에서 제거하는 방법은 연산을 취소하는 방법뿐이다. 취소하는 방법에는 연산 객체(Operation Object)의 `cancel()` 메소드를 호출하거나 Operation Queue의 `cancellAllOperations()` 메서드를 호출하여 대기열에 있는 모든 연산을 취소하는 방법이 있다. 그리고 실행 중인 연산의 경우, 연산 객체의 취소 상태를 확인하고 실행 중인 연산을 중지하고 완료 상태로 변경된다.

# 연산 객체(Operation Object)

애플리케이션에서 수행하려는 연산을 캡슐화하는 데 사용하는 `Foundation` 프레임워크의 `Operation` 클래스 인스턴스.

# OperationQueue의 주요 메서드/프로퍼티

### 특정 Operation Queues 가져오기

- current: 현재 작업을 시작한 Operation Queue를 반환한다.
- main: 메인 스레드와 연결된 Operation Queue를 반환한다.

### 대기열(Queue)에서 동작(Operation) 관리

- addOperation(_:) : Operation Object를 Queue에 추가한다.
- addOperations(_:waitUntilFinisehd:) : Operation Object 배열을 Queue에 추가한다.
- addOperation(_:) : 전달한 클로저를 Operation Object에 감싸서 Queue에 추가한다.
    
    ```swift
    func addOperation(_ block: @escaping () -> Void)
    ```
    
- cancelAllOperations() : 대기 중이거나 실행 중인 모든 연산을 취소한다.
- waitUntilAllOperationsAreFinished() : 대기 중인 모든 연산과 실행 중인 연산이 모두 완료될 때까지 현재 스레드로의 접근을 차단한다.

### 연산(Operation) 실행 관리

- maxConcurrentOperationCount: 동시에 실행할 수 있는 연산의 최대 수
- qualityOfService: 대기열 작업을 효율적으로 수행할 수 있도록 여러 우선순위 옵션을 제공한다.

### 연산(Operation) 중단

- isSuspended: 큐의 연산 여부를 나타내기 위한 Bool 값. false인 경우 큐에 있는 연산을 실행하고, true인 경우 큐에 대기 중인 연산을 실행하진 않지만 이미 실행 중인 연산은 계속 실행된다.

### Queue의 구성

- name: Operation Queue의 이름
