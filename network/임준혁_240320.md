# handshake

## 3 way handshake
c : client
s : server

1. c -> s, syn(a)
2. s -> c, ack(a+1), syn(b)
3. c -> ack(b+1)
   서로가 응답을 확인해야 하기 때문에 3 way handshake여야 함.

## 4 way handshake
1. c -> s, fin flag
2. s -> c, ack. s time out
3. s -> c, fin
4. c -> s, ack
5. s, socket close
6. c, time wate
   서버는 보낼 데이터가, 클라이언는 받을 데이터가 있을 수 있기 때문에 바로 종료하지 않는다.

# TCP UDP

UDP : user datagram protocol. 비연결형. ip 데이터그램을 캡슐화하여 전송. 연결, 흐름제어, 손상 세그먼트 재전송 없음. 
TCP : transmission control protocol. 신뢰성, 순차 전달 제공. 
- - 흐름제어 : 송신이 빠를 때 수신자의 버퍼에서 손실 발생 가능. 소신가자 받는 패킷 수를 조절. stop and wait(매번 확인 후 전송), sliding window(윈도우 크기만큼 전송)
- - 혼잡제어 : 네트워크의 전송 속도 문제 해결. aimd(additive increase, multimplicative decrease) 패킷의 개수를 1개씩 증가. 시간 초과시 절반으로 감소
  - -- slow start : 초기 속도 문제 보완. ack 1개당 윈도우 사이즈 1 증가. 즉, 1주기당 2배로 증가. 혼잡시 1로 복귀. 그후, 과서 사이즈 절반까지 지수적으로 증가. 절반부터 1씩 증가.
  
