# 네트워크의 전체 흐름


## 네트워크의 구성

- 응용 계층: 애플리케이션 등에서 사용하는 데이터를 송수신 하는데 필요
- 전송 계층: 목적지에 데이터를 정확하게 전달
- 네트워크 계층: 다른 네트워크에 있는 목적지에 데이터를 전달
- 데이터 링크 계층: 랜에서 데이터를 송수신
- 물리 계층: 데이터를 전기 신호로 변환

---

## 데이터 → 전기 신호


### 응용계층

- URL 입력 → 캡슐화가 시작
- HTTP 프로토콜을 사용하여 전송 계층으로 메시지가 보내진다.
- 전송 계층에서는 데이터에 TCP 헤더가 붙어 세그먼트가 된다.
    - 출발지 포트 번호는 1025번 이상인 포트 중에서 무작위로 선택된다
    - 목적지 포트 번호는 보통 80번 포트가 된다.
- 네트워크 계층에서는 전달받은 세그먼트에 IP 헤더가 붙는다. → IP 패킷
    - 출발지 IP, 목적지 IP주소가 추가된다.
- 데이터 링크 계층에서는 이더넷 헤더가 추가된다. → 이더넷 프레임
    - 출발지, 목적지 MAC 주소 추가
- 물리 계층에서 랜카드를 이용하여  전기 신호로 변환된다.

---

## 스위치와 라우터에서의 데이터 전달, 처리

### 스위치에서

데이터 링크 계층에서 데이터를 전기 신호로 변환하여 라우터로 전송한다.

### 라우터에서

데이터 링크 계층에서 이더넷 프레임의 목적지 MAC 주소와 자신의 MAC 주소를 비교한다.

비교 후 같으면 이더넷 헤더와 트레일러를 분리한다.(역캡슐화)

네트워크 계층에 전달 후 라우팅 테이블과 목적지 IP 주소 비교

라우팅 테이블에서 목적지 IP 주소의 경로를 알 수 있으면 라우팅

라우터 B는 데이터가 도착하면 목적지 MAC 주소와 자신의 MAC wnth qlry

비교 후 같으면 이더넷 헤더와 트레일러 분리(역캡슐화)

데이터가 스위치 B로 전달 → 웹 서버에 데이터를 전기 신호로 전달

---

## 웹 서버에서 데이터 전달, 처리

물리 계층에서 전기 신호로 변환된 데이터 수신

데이터 링크 계층에서 이더넷 프레임의 목적지 MAC 주소와 자신의 MAC 주소 비교

비교 후 같으면 이더넷 헤더와 트레일러 분리

네트워크 계층에 전달 후 라우팅 테이블과 웹서버 IP 주소 비교

같으면 IP 헤더 분리 후 전송 계층으로 전송

목적지 포트 번호 확인

TCP 헤더 분리, 응용 계층에 전달

애플리케이션에서 사용

---