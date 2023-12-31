# Network Layer

> 데이터를 연결하는 다른 네트워크를 통해 전달함으로써 인터넷이 가능하게 만드는 계층
> 
> - **주소부여(IP)**
> 
> - **경로설정(Route)**
> 
> - 

- 역할
  
  - 경로를 선택하고 주소를 정하고 경로에 따라 패킷을 전달해주는 것
  
  - 여러개의 노드를 거칠때마다 경로를 찾아주는 역할
  
  - 라우팅, 흐름 제어, 세그멘테이션(segmentation/desegmentation), 오류 제어, 인터네트워킹(Internetworking) 등을 수행

- 대표 장비 
  
  - 라우터 
  
  - 2계층의 장비 중 스위치라는 장비에 라우팅 기능을 장착한 Layer 3 스위치도 있음

## 라우팅

> 라우팅은 네트워크에서 경로를 선택하는 프로세스

- 컴퓨터 네트워크는 *노드*라고 하는 여러 시스템과 이러한 노드를 연결하는 경로 또는 링크로 구성

- 상호 연결된 네트워크에서 두 노드 간의 통신은 여러 경로를 통해 이루어질 수 있습니다. 라우팅은 미리 정해진 규칙을 사용하여 최상의 경로를 선택하는 프로세스

- 라우팅은 2가지 유형으로 구분

### 정적 라우팅

- 네트워크 관리자가 정적 테이블을 사용하여 네트워크 경로를 수동으로 구성하고 선택

- 네트워크 설계나 파라미터가 일정하게 유지될 것으로 예상되는 경우에 유용

### 동적 라우팅

- 실제 네트워크 조건에 따라 런타임에 라우팅 테이블을 만들고 업데이트

- 동적 라우팅 테이블을 만들고 유지 관리하고 업데이트하는 규칙 집합인 동적 라우팅 프로토콜을 사용하여 소스에서 대상까지 가장 빠른 경로를 찾으려고 시도

- 장점 
  
  -  트래픽 볼륨, 대역폭, 네트워크 장애 등 변화하는 네트워크 조건에 대응한다는 것

### 라우팅 프로토콜

> 라우터가 패킷을 식별하고 네트워크 경로를 따라 전달하는 방법을 지정하는 규칙 세트

- 내부 게이트웨이 프로토콜과 외부 게이트웨이 프로토콜이라는 2가지 범주로 분류

- 내부 게이트웨이 프로토콜 
  
  - 단일 조직에서 관리자가 제어하는 네트워크인 자율 시스템에서 가장 효괴적으로 작동
  
  - 평가지표 
    
    - 홉 수 또는 소스와 대상 간의 라우터 수
    - 지연 또는 소스에서 대상으로 데이터를 전송하는 데 걸린 시간
    - 대역폭 또는 소스와 대상 간의 링크 용량
  
  - 종류 
    
    - **Routing Information Protocol**
      
      -  홉 수를 기준으로 네트워크 간의 최단 경로를 결정
      
      - 대규모 네트워크를 구현하는 데 적합하지 않음
    
    - **Open Shortest Path First 프로토콜**
      
      - 자율 시스템의 다른 모든 라우터에서 정보를 수집하여 데이터 패킷의 대상까지 가장 짧고 빠른 경로를 식별

- 외부 게이트웨이 프로토콜 
  
  - 두 자율 시스템 간의 정보 전송을 관리하는 데 보다 적합
  
  - 종류
    
    - **Border Gateway Protocol(BGP)**
      
      - 인터넷(서로 모두 연결되어 있는 대규모 자율 시스템의 모음)을 통한 통신을 정의
      
      - 모든 자율 시스템에는 Internet Assigned Numbers Authority에 등록하여 할당받는 Autonomous System Number(ASN)가 있음
      
      - BGP는 가장 가까운 ASN을 추적하고 대상 주소를 해당 ASN에 매핑하는 방식으로 작동

### 라우팅 알고리즘

>  라우팅 알고리즘은 다양한 라우팅 프로토콜을 구현하는 소프트웨어 프로그램

각 링크에 비용 수치를 할당하는 방식으로 작동

비용 수치는 다양한 네트워크 지표를 사용하여 계산됨

모든 라우터는 데이터 패킷을 최저 비용으로 차선의 링크에 전달하려고 시도

#### 알고리즘 예시

##### 거리 벡터 라우팅

- 모든 라우터가 각각 찾은 최상의 경로 정보를 주기적으로 서로 업데이트

- 각 라우터는 총 비용의 현재 평가 결과에 대한 정보를 알려진 모든 대상으로 보냄
  
  결국 네트워크의 모든 라우터는 가능한 모든 대상에 대한 최상의 경로에 대한 정보를 찾게 됨

##### 링크 상태 라우팅

- 모든 라우터가 네트워크의 다른 모든 라우터를 검색

- 라우터는 이 정보를 사용하여 전체 네트워크의 맵을 만든 다음 데이터 패킷의 최단 경로를 계산

### 클라우드 라우팅

> 두 가상 클라우드 네트워크 간 또는 클라우드 네트워크와 온프레미스 네트워크 간의 연결을 동적으로 관리

### DNS 라우팅

> [도메인 이름 시스템(DNS)](https://aws.amazon.com/route53/what-is-dns/)은 사람이 읽을 수 있는 도메인 이름(예: [www.naver.com](https://www.naver.com/))을 시스템이 읽을 수 있는 IP 주소(예: 192.0.2.44)로 변환

## 라우터

> 컴퓨팅 디바이스와 네트워크를 다른 네트워크에 연결하는 네트워킹 디바이스

- 기본기능 
  
  - 경로 결정 
    
    - 소스에서 대상으로 이동하는 데이터의 경로를 결정
    
    - 지연, 용량 및 속도와 같은 네트워크 지표를 분석하여 최상의 경로를 찾으려고 시도
  
  - 데이터 전달 
    
    - 선택한 경로의 다음 디바이스로 데이터를 전달하여 최종적으로 대상에 도달하도록 함
  
  - 로드밸런싱
    
    - 여러 경로를 사용하여 동일한 데이터 패킷의 여러 사본을 전송할 수도 있음
    
    - 데이터 손실로 인한 오류를 줄이고 이중화를 구현하고 트래픽 볼륨을 관리

## TCP/IP

> 인터넷 프로토콜 IP + 전송 조절 프로토콜 TCP

- IP주소 체계를 따라 IP라우팅을 통해 목적지에 도달해서 TCP의 특성을 이용해 송신자와 수신자의 논리적 연결을 생성하고 신뢰성을 유지 

### IP 계층

TCP/IP 상에서 IP 계층이란 네트워크의 주소 (IP 주소)를 정의하고,  

**IP 패킷의 전달 및 라우팅을 담당하는 계층**

OSI 7계층모델의 관점에서 보면  IP 계층은 네트워크계층에 해당

- 즉, 패킷을 목적지까지 전달하는 역할 및 그에 수반되는 기타 역할을 함

IP 계층의 주요 역할

- IP 계층에서는 그 하위계층인 데이터링크 계층의 하드웨어적인 특성에(즉, ATM 이 든 Frame Relay 이든 상관없이) 

관계없이 독립적인 역할을 수행

IP 계층 상에 있는 주요 프로토콜

- 패킷의 전달을 책임지는 IP

- 패킷 전달 에러의 보고 및 진단을 위한 ICMP

- 복잡한 네트워크에서 인터네트워킹을 위한 경로를 찾게해주는 라우팅 프로토콜

### IP 프로토콜

- TCP/IP 기반의 인터넷 망을 통하여 데이타그램의 전달을 담당하는 프로토콜
1. 주요 기능

IP 계층에서 IP 패킷의 라우팅 대상이 됨 (Routing)

IP 주소 지정 (Addressing)

2. 주요 특징
- `신뢰성(에러제어)` 및 `흐름제어`  기능이 전혀 없음  -> Best-Effort Service

     - 한편, 신뢰성을 확보하려면 IP 계층 위의 TCP와 같은 상위 트랜스포트 계층에 의존

- 비연결성 데이터그램 방식으로 전달되는 프로토콜  ->  Connectionless

- 패킷의 완전한 전달(소실,중복,지연,순서바뀜 등이 없게함)을 보장 않음  ->  Unreliable

- IP 패킷 헤더 내 수신 및 발신 주소를 포함  ☞ IPv4 헤더, IPv6 헤더, IP 주소

- IP 헤더 내 바이트 전달 순서 : 최상위 바이트(MSB)를 먼저 보냄  -> Big-endian 

- 경우에따라, 단편화가 필요함  -> IP 단편화 참조

- TCP, UDP, ICMP, IGMP 등이 IP 데이타그램에 실려서 전송

# Transport Layer

>  통신을 활성화하기 위한 계층  

- 보통 TCP프로토콜을 이용하며, 포트를 열어서 응용프로그램들이 전송을 할 수 있게 함

- 만약 데이터가 왔다면 4계층에서 해당 데이터를 하나로 합쳐서 5계층에 던져 줌

- 전송 계층(Transport layer)은 양 끝단(End to end)의 사용자들이 신뢰성있는 데이터를 주고 받을 수 있도록 해 주어,  상위 계층들이 데이터 전달의 유효성이나 효율성을 생각하지 않도록 해줌

- 시퀀스 넘버 기반의 오류 제어 방식을 사용

- 전송 계층은 특정 연결의 유효성을 제어하고, 일부 프로토콜은 상태 개념이 있고(stateful),  **연결 기반(connection oriented)** 
  
  이는 **전송 계층이 패킷들의 전송이 유효한지 확인하고 전송 실패한 패킷들을 다시 전송한다는 것**을 뜻함

- 가장 잘 알려진 전송 계층의 예는 TCP
  
  - 종단간(end-to-end) 통신을 다루는 최하위 계층으로 종단간 신뢰성 있고 효율적인 데이터를 전송하며, 기능은 오류검출 및 복구와 흐름제어, 중복검사 등을 수행

-> **패킷 생성(Assembly/Sequencing/Deassembly/Error detection/Request repeat/Flow control) 및 전송**

### TCP 프로토콜(Transmission Control Protocol)

OSI 계층모델의 관점에서 전송 계층(4계층)에 해당

양종단 호스트 내 프로세스 상호 간에 신뢰적인 연결지향성 서비스를 제공

- IP의 비신뢰적인 최선형 서비스에다가 신뢰적인 연결지향성 서비스를 제공하게 됨

. **신뢰적인 전송을 보장**함으로써, 어플리케이션 구현이 한층 쉬워지게 됨

**1. 신뢰성 있음 (Reliable)**

패킷 손실, 중복, 순서바뀜 등이 없도록 보장

TCP 하위계층인 IP 계층의 신뢰성 없는 서비스에 대해 다방면으로 신뢰성을 제공

**2. 연결지향적 (Connection-oriented)**                                

같은 전송계층의 UDP가 비연결성(connectionless)인 것과는 달리, TCP는 연결지향적임

이 경우, 느슨한 연결(Loosly Connected)을 갖으므로 강한 연결을 의미하는 가상회선이라는 표현 보다는 오히려 연결지향적이라고 말함

연결 관리를 위한 연결설정 및 연결해제 필요 -> TCP 연결설정, TCP 연결종료

양단간 어플리케이션/프로세스는 TCP가 제공하는 연결성 회선을 통하여 서로 통신

### UDP 프로토콜(User Datagram Protocol)

전송 계층의 통신 프로토콜의 하나 (TCP에 대비됨)

- **신뢰성이 낮은 프로토콜**로써 완전성을 보증하지 않으나,  

- 가상회선을 굳이 확립할 필요가 없고 유연하며 효율적 응용의 데이타 전송에 사용

**1. 비연결성이고, 신뢰성이 없으며, 순서화되지 않은 Datagram 서비스 제공** 

- 메세지가 제대로 도착했는지 확인하지 않음 (확인응답 없음)

- 수신된 메세지의 순서를 맞추지 않음 (순서제어 없음) 

- 흐름 제어를 위한 피드백을 제공하지 않음 (흐름제어 없음)

- 검사합을 제외한 특별한 오류 검출 및 제어 없음 (오류제어 거의 없음)

UDP를 사용하는 프로그램 쪽에서 오류제어 기능을 스스로 갖추어야 함

- 데이터그램 지향의 전송계층용 프로토콜 (논리적인 가상회선 연결이 필요없음)

비연결접속상태 하에서 통신 

**2. 실시간 응용 및 멀티캐스팅 가능**

- 빠른 요청과 응답이 필요한 실시간 응용에 적합

- 여러 다수 지점에 전송 가능 (1:多)

**3. 헤더가 단순함**

- UDP는 TCP 처럼 16 비트의 포트 번호를 사용하나,

- 헤더는 고정크기의 8 바이트(TCP는 20 바이트) 만 사용

즉, 헤더 처리에 많은 시간과 노력을 요하지 않음
