# CPU 스케줄링의 목적은 무엇인가

---

CPU 스케줄링의 목적은 CPU를 효율적이고 공정하게 사용하는 것이다.
이를 위해 다음과 같은 지표들이 사용된다.  
- turnaround time: 프로세스가 도착해서 끝날 때까지 걸리는 시간
- waiting time: 프로세스가 CPU를 받지 않고 대기만 한 시간(turnaround time - burst time(CPU를 사용한 시간))
- response time: 프로세스가 들어와서 실행되기까지 걸리는 시간

# 꼬리 질문

---

## 선점형과 비선점형 스케줄링의 예에 대해서 하나씩 들어주세요

--- 

선점형은 현재 CPU 권한을 할당 받은 프로세스의 모든 작업이 끝나기 전에 다른 프로세스가 CPU 권한을 빼앗을 수 있는 스케줄링이다.  
비선점형은 그 반대로 현재의 프로세스가 끝나기 전까지 다른 프로세스가 CPU를 사용할 수 없다.   

선점형 스케줄링에는 다음의 것들이 있다.   

### Priority Scheduling
- 우선순위를 정해준 대로 프로세스를 실행한다.
- 높은 우선순위 작업이 들어가면 교체된다.
- 우선순위에 맞게 진행하기 때문에 더 중요한 작업에 대한 turnaround, waiting time이 줄어든다.
- but 우선순위가 낮은 태스크는 starvation이 생김 공정성의 문제가 생긴다.

### Round robin
- 사용하기 쉽고 구현하기 간단하다.
- CPU 스케줄링에서 많이 사용되는 방법 중 하나이다.
- 반응 시간이 짧아진다.
- 공정하다.
- 단점은 스위칭에 따른 오버헤드가 존재한다.

### Shortest Remaining Time First
- SJF의 선점형 버전이다.
- 더 적게 남은 태스크에게 CPU를 할당한다.
- 프로세스가 끝나거나 새로운 프로세스가 들어왔을 때 결정하기 때문에 스위칭에 대한 오버헤드가 적다.
- 하지만 긴 작업은 starvation 문제가 발생한다.

### Multilevel Feedback Queue
- 여러 우선순위 큐로 나눈다.
- 먼저 제일 높은 우선순위에 갔다가 인터럽트가 걸렸는데 끝나지 않으면 아래 큐로 떨어지는 방식이다.
- 같은 레벨에서는 round robin 방식을 사용한다. 
- 유연하다
- 가장 복잡하다.

비선점형에는 다음의 것들이 있다.

### FCFS
- 구현하기 쉽다
- 작업 오래 걸리는 프로세스가 먼저 오게 되면 turnaround time이 길어진다. (convoy effect or starvation)

### SJF
- 짧은 작업 먼저 오도록 한다.
- 다른 스케줄링보다 가장 낮은 평균 대기 시간을 가진다.
- turnaround 시간이 작아진다.
- 긴 작업은 starvation 문제가 발생한다.
- long term scheduling에 사용된다.
- 누가 작게 걸릴지 알 수가 없다.

### Highest Response Ratio Next:
- 가장 최적화 알고리즘으로 평가된다.
- 가장 높은 응답 비율을 가진 프로세스를 먼저 실행한다.
- SJF에서의 starvation 문제를 해결하기 위한 방안이다.
- Response Ratio = (W + S) / S
- SJF보다 더 좋은 성능을 가진다.
- burst time을 알 방법이 없다.


### Reference

---
- https://www.geeksforgeeks.org/cpu-scheduling-in-operating-systems/﻿
