# Operating System

### 선점, 비선점 스케줄링

- 비선점
    
    → 프로세스가 자원을 할당 받았을 경우, 자원을 스스로 반납할 때까지 계속 그 자원을 사용하도록 허용하는 정책
    
- 선점
    
    → 쓰다가 멈추고 쓰다가 멈추고...
    
    → context switch 자주일어나서 오버헤드가 높다.

### Round Robin

스케줄링 기법의 하나. 

모든 job은 `quantum` 이라는 time slice 를 가지고 해당 시간동안만 수행함.

  → 문제점: quantum이 길면 response time이 떨어지고, 너무 짧으면 context swtich 자주.
  
### Critical section (aka Critical Region)

스레드들이 공유된 자원에 대해서 접근하기 위해 경쟁하는 상태: `Race condition`

그런 공유된 자원을 다루는 부분: `Critical Section`

#### 해결 방법

1. Lock 변수
    1. lock이 0일때 cs 진입 가능, 1이면 수행하지 않음. 즉 1이면 누군가 수행중.
    2. 단점
        1. 프로세스 A와 B가 있는데,
            
            A가 Lock 변수가 0일때 진입하는 순간, B로 context swtich 되어 B에서 Lock이 1로 설정→ 그리고 A로 돌아오면 A는 CS에 진입. 
            
2. Lock with sleep and wakeup
    1. sleep 시키고 lock이 0되면 wakeup.
3. TSL (Test and Set Lock) (== Test And Set )
    
    atomic 한 instuction 과 lock 변수를 통해서 제어.
    
4. Semaphore
    
    lock 변수보다 higher level. 다익스트라가 만듬. / 공유 자원의 개수를 나타내는 변수.
    
    P연산(wait): semaphore를 1 감소 / V연산(signal): semaphore를 1 증가
    
    ❗ 감소시켰는데 semaphore가 음수라면 wait() 를 부른 프로세스는 sleep.
    
    ❗ 증가시켰는데 semaphore가 0이나 음수면 자는애들 깨워야함.
    
5. Mutex
    
    binary semaphore.
