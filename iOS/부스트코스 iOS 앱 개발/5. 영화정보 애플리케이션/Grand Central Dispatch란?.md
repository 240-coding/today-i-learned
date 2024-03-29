# Grand Central Dispatch(GCD)

Grand Central Dispatch(GCD)는 멀티코어와 멀티 프로세싱 환경에서 최적화된 프로그래밍을 할 수 있도록 애플이 개발한 기술이다. 기본적으로 스레드 풀의 관리를 프로그래머가 아닌 운영체제에서 관리하기 때문에 프로그래머가 태스크를 비동기적으로 쉽게 사용할 수 있다. 프로그래머가 실행할 태스크를 생성하고 `Dispatch Queue` 에 추가하면 GCD는 태스크에 맞는 스레드를 자동으로 생성해서 실행하고 작업이 종료되면 해당 스레드를 제거한다. 

### 디스패치 대기열(Dispatch Queue)

Dispatch Queue는 작업을 연속적 혹은 동시에 진행하기는 하지만, 언제나 먼저 들어오면 먼저 나가는 순서로 실행된다. `Serial Dispatch Queue` 는 한 번에 하나의 작업만을 실행하며, 해당 작업이 대기열에서 제외되고 새로운 작업이 시작되기 전까지 기다린다. 이와는 반대로 `Concurrent Dispatch Queue`는 이미 시작된 작업이 완료될 때까지 기다리지 않고 가능한 많은 작업을 진행한다. 디스패치 대기열은 GCD 기술의 일부이다.

### Dispatch Source

Dispatch Source는 특정 유형의 시스템 이벤트를 비동기적으로 처리하기 위한 C 기반 매커니즘이다. 특정 유형의 시스템 이벤트에 대해 정보를 캡슐화하고, 해당 이벤트가 발생할 때마다 특정 클로저(블록) 객체 혹은 기능을 Dispatch Queue에 전달한다. DIspatch Source는 GCD 기술의 일부이다.

### 연산 대기열(Operation Queue)

Operation Queue는 `Concurrent Dispatch Queue` 와 동일하게 동작하며, `Operation Queue` 클래스에 의해 구현된다. 디스패치 대기열은 항상 먼저 들어오면 먼저 나가는 순서(FIFO)로 작업을 실행하지만, 연산 대기열(Operation Queue)는 작업의 실행 순서를 결정할 때 다른 요인들을 고려한다. Operation Queue는 Dispatch Queue와 매우 유사한 클래스이다.

### GCD와 연산 대기열(Operation Queue)

- 차이점
    - Operation Queue에서는 동시에 실행할 수 있는 Operation의 최대 수를 지정할 수 있다.
    - Operation Queue에서는 KVO(Key Value Observing)을 사용할 수 있는 많은 프로퍼티들이 있다.
    - Operation Queue에서는 연산(Operation)을 일시 중지, 다시 시작 및 취소를 할 수 있다.

### 언제 사용해야 할까?

- Operation Queue: 비동기적으로 실행되어야 하는 작업을 객체 지향적인 방법으로 사용하는 데 적합하다. KVO(Key Value Observing)를 사용해 작업 진행 상황을 감시하는 방법이 필요할 때도 적합하다.
- GCD: 작업이 복잡하지 않고 간단하게 처리하거나 특정 유형의 시스템 이벤트를 비동기적으로 처리할 때 적합하다. 예를 들면 타이머, 프로세스 등의 관련 이벤트이다.
