# CS 인터뷰

<details>
<summary>토글</summary>
<div markdown="1">

안녕

</div>
</details>

## 웹 전반(자바 스프링, 디자인 패턴, 인프라 등)


    

## 운영체제



<details>
<summary>프로세스와 스레드의 차이</summary>
<div markdown="1">

    프로세스는 실행 중인 프로그램으로 운영체제에서 자원을 할당하는 주체가 된다
    스레드는 프로세스의 실행 단위이다. 같은 프로세스에 속한 스레드는 주소 공간, 자원 등을 공유한다.

    스택과 PC Register는 스레드 마다 독립적으로 할당한다.

    스택은 함수 호출 시 전달되는 인자, 되돌아갈 주소값, 함수 내에서 선언하는 변수 등을 저장하기 위해 사용됨
    → 스레드의 독립적인 실행 흐름을 추가하기 위해

    PC Register는 스레드가 명령어의 어디까지 실행했는지를 저장한다.
    → 스케줄러에 의해 불연속적으로 스레드가 실행될 때 명령어가 어느 부분까지 실행됐는지 기억할 필요가 있다.

</div>
</details>

    
<details>
<summary>멀티 스레드</summary>
<div markdown="1">

    - 장점
    
    스레드 간 통신이 필요한 경우 전역 변수의 공간 혹은 Heap을 공유하기 때문에 보다 간단하게 데이터를 주고 받을 수 있다.
    
    Context switch가 발생할 경우 캐시 메모리를 비울 필요가 없기 때문에 overhead가 적다.
    
    - 문제점
    
    동일한 자원에 여러 프로세스가 접근할 경우 동기화 작업이 필요하다
    mutex lock을 사용할 경우 병목현상이 발생하여 성능이 저하될 가능성이 높다
    
    - 멀티 프로세스와의 차이
    
    멀티 스레드의 경우 하나의 스레드가 오류로 인해 종료되면 다른 스레드 또한 영향을 받는다.
    
    반면 멀티 프로세스의 경우 하나의 프로세스가 죽어도 다른 프로세스에는 영향을 끼치지 않는다.
    
    다만 멀티 스레드를 사용하는 경우보다 메모리와 cpu 시간을 더 많이 차지한다는 단점이 존재한다.

</div>
</details>
    

<details>
<summary>컨텍스트 스위칭이란?</summary>
<div markdown="1">

    cpu를 한 프로세스에서 다른 프로세스로 넘겨 주는 과정이다.
    
    SYS call 이나 interrupt가 발생하면 (반드시는 아니지만) 컨텍스트 스위칭이 발생한다.
    현재 프로세스의 상태를 PCB에 저장하고 새로운 프로세스의 상태를 레지스터에 저장한다.
    
    프로세스의 컨텍스트 스위칭의 경우 cpu memory flush가 발생하면 오버헤드가 커진다.

</div>
</details>


 


## 네트워크



## DB


## 자료구조


## 알고리즘