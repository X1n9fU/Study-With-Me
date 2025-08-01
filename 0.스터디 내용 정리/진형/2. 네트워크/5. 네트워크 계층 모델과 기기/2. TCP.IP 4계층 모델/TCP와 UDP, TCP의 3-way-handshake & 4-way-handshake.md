# TCP와 UDP: 3-way 핸드셰이크와 4-way 핸드셰이크

> 정의 : TCP와 UDP는 전송 계층 프로토콜로, 연결 설정 및 해제 방식에서 큰 차이가 있습니다.  
아래에서는 TCP의 **3-way 핸드셰이크**(연결 설정)와 **4-way 핸드셰이크**(연결 해제), 그리고 UDP의 특성을 정리합니다.
---

## 1. TCP 특징

- 연결 지향 방식으로 패킷 교환 방식을 사용한다(가상 회선 방식이 아님).
- 3-way handshaking과정을 통해 연결을 설정하고 4-way handshaking을 통해 해제한다.
- 흐름 제어 및 혼잡 제어.
- 높은 신뢰성을 보장한다.
- UDP보다 속도가 느리다.
- 전이중(Full-Duplex), 점대점(Point to Point) 방식.

---

## 2. TCP 3-way 핸드셰이크 (연결 설정)

### 정의  
클라이언트와 서버가 신뢰성 있는 연결을 맺기 위해 3단계로 **SYN, SYN-ACK, ACK** 메시지를 교환하는 절차입니다.

### 단계  
1. **SYN** (Client → Server)  
   - 클라이언트가 서버에 연결 요청을 보낼 때, 초기 시퀀스 번호(ISN)를 포함한 SYN 플래그가 설정된 TCP 세그먼트를 전송합니다.  
2. **SYN-ACK** (Server → Client)  
   - 서버는 클라이언트의 SYN 요청을 받고, 자신의 초기 시퀀스 번호와 함께 ACK(클라이언트 ISN+1)를 포함한 SYN-ACK 세그먼트를 돌려보냅니다.  
3. **ACK** (Client → Server)  
   - 클라이언트는 서버의 SYN-ACK을 수신하고, 서버 ISN+1을 ACK로 응답하여 연결이 확립됩니다.  

### 특징  
- 양방향 시퀀스 번호 교환을 통해 양쪽 모두 연결 의사를 확인  
- 중간에 손실된 패킷 재전송 메커니즘으로 신뢰성 보장  

---

## 3. TCP 4-way 핸드셰이크 (연결 해제)

### 정의  
TCP 연결을 안전하게 종료하기 위해 FIN과 ACK 메시지 4단계를 거치는 절차입니다.

### 단계  
1. **FIN** (Client → Server)  
   - 클라이언트가 더 이상 데이터를 보내지 않겠다는 FIN 플래그를 포함한 세그먼트를 전송합니다.  
2. **ACK** (Server → Client)  
   - 서버는 FIN을 받고, 클라이언트 시퀀스 번호+1을 ACK로 응답합니다.  
3. **FIN** (Server → Client)  
   - 서버 측도 데이터 전송이 끝났음을 알리기 위해 FIN 플래그를 포함한 세그먼트를 전송합니다.  
4. **ACK** (Client → Server)  
   - 클라이언트는 서버 FIN을 확인하고, 서버 시퀀스 번호+1을 ACK로 응답하며 연결이 완전히 종료됩니다.  

### 특징  
- 각 방향(클라이언트→서버, 서버→클라이언트)의 종료 의사를 별도로 확인  
- TIME-WAIT 상태를 둬서 지연된 패킷 재전송 처리를 보장  

---

## 4. UDP (User Datagram Protocol)

### 정의 및 특성  
- **비연결형(Connectionless)** 전송 계층 프로토콜  
- **핸드셰이크 과정 없음**: 세션 설정이나 종료를 위한 제어 메시지를 교환하지 않음  
- **장점**: 오버헤드가 적어 빠른 전송 가능, 실시간 스트리밍·VoIP 등에 적합  
- **단점**: 패킷 순서 보장·재전송·흐름 제어 기능 부재 — 애플리케이션에서 직접 처리 필요  

---

> **참고**:  
> - TCP는 연결 지향형 프로토콜로, 3-way 핸드셰이크와 4-way 핸드셰이크 절차로 신뢰성과 순서 보장을 제공합니다.  
> - UDP는 경량·비연결형으로, 빠른 전송이 필요한 서비스에 주로 사용됩니다.

Reference
출처: https://mangkyu.tistory.com/15 [MangKyu's Diary:티스토리]
