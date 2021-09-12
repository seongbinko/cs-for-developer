## CPU scheduling

### 1. CPU burst vs IO burst

<img width="426" alt="스크린샷 2021-09-12 오전 11 52 02" src="https://user-images.githubusercontent.com/66991236/132969848-335a6185-f7b2-43fe-ad26-64673454a068.png">


1) CPU burst 
   : CPU가 사용되는 단계
   * CPU-Bound Process
     : CPU 연산은 많은데 사용자와의 Interaction이 적은 프로그램
     
2) IO burst 
   : IO 작업을 하는 과정  
   * I/O-Bound Process
      : CPU 연산은 적은데 사용자와의 Interaction이 많은 프로그램.


### 2. CPU 스케쥴링
 IO bound가 사람과 인터렉션하는 job인데, 이런 job에 cpu를 늦게 할당하게 되면 >> 사람이 너무 오개리다리게 됨
 그래서 현재 큐에 들어와있는 cpu를 얻고자 하는 프로세스들 중에 어떤 프로세스에 cpu를 줘야하는지 결정하는 과정이 cpu 스케쥴링
 
 * CPU 스케쥴링의 2가지 이슈
 1) cpu burst 에 들어온 프로그램이 여럿인데 누구한테 cpu를 줄 것인가
 2) cpu를 프로그램에 줬으면 이 프로그램이 cpu를 다 쓰고 io하러 나갈 때 까지 cpu를 계속 주어야 하는지, 아니면 중간에 cpu를 뺐어서 다른 프로세스한테 넘겨줘야하는지
  
### 3. cpu 알고리즘
  1) 비선점형 : 하나의 프로세스가 끝나지 않으면 다른프로세스는 CPU를 사용할 수 없음
  2) 선점형 : 하나의 프로세스가 다른 프로세스 대신에 프로세서(CPU)를 차지할 수 있음.

둘 중에 어떤 것이 더 좋은 성능을 내는지 평가할 수 있는 방법이 필요하고, 이를 성능척도 라고 부름

### 4. 성능척도
  1) 시스템 입장
    - 시스템 하나 가지고 최대한 일을 많이 시키면 좋음
    
  2) 프로그램 입장 
    - 내가 빨리 cpu 얻어서 빨리 끝내면 좋음
    
  
  * 시스템 입장
    1) cpu utilization (이용률)
     - 전체 시간 중에서 cpu가 놀지 않고 일한 시간의 비율 > cpu를 가능한 놀지 않게 일을 시켜라 
    
    2) throughput (처리량 / 산출량)
     - 주어진 시간 동안에 과연 몇개의 일을 처리했느냐
     
  * 프로그램입장
    1) turnaround time
      - cpu를 쓰러 들어와서 다 쓰고 나갈 때까지 걸린 시간 > i/o 하러 나갈 때까지 걸린 시간
    
    2) waiting time
      - CPU가 서비스를 받기 위해 Ready Queue에서 얼마나 기다렸는지      

    3) response time
      - cpu쓰겠다고 들어와서 처음으로 cpu쓰기까지 걸린 시간 
      
### 5. cpu스케쥴링 알고리즘
 1) FCFS (first come first served)
   - 먼저 온 순서대로 처리
   - 단점 : cpu를 오래 쓰는 프로그램이 먼저 도착해서 cpu를 쓰고 있으면 아주 짧게 cpu를 쓰고 나갈 프로그램이더라도 오래 기다려야함
   - 즉, 앞에 어떤 프로세스가 있냐에 따라 기다리는 시간에 영향을 미침
      > 이렇게 긴 프로세스가 먼저 도착해서 짧은 프로세스가 오래 기다리는 현상
         convoy effect 라고 함
         
 3) SJF (Shortest Job first)
   - average waiting time을 최소화 하는 알고리즘
   - cpu를 사용하고자 하는 시간이 제일 짧은 프로그램한테 cpu를 줌
     그러나 이 알고리즘도 단점이 있음
     1. starvation 
     2. cpu burst time을 알 수 없음
