# Stack

## 시스템 stack 함수 호출

- System Stack : 운영체제가 사용하는 스택 

![](https://velog.velcdn.com/images/eoveol/post/46698f3d-03b8-4b34-bdb0-15add00903f5/image.png)

- 복귀주소 기억 
  - 함수는 실행이 끝나면 자신을 호출한 함수로 되돌아감. 이 때 복귀할 주소를 기억하는 데 사용 

![](https://velog.velcdn.com/images/eoveol/post/e2fafd47-3943-45c6-b847-658d1ac33432/image.png)

- 활성 레코드 
  - 시스템 스택에는 함수가 호출될 때마다 활성 레코드(activation record)가 만들어지며, 이곳에 복귀주소가 저장됨 
  - 활성 레코드에 생성되는 정보 
    - 복귀 주소 
    - 프로그램 카운터 
    - 매개변수 
    - 함수 안에서 선언된 지역 번수 

## 스택 추상 자료형

> LIFO인 선형리스트의 일종 

![](https://velog.velcdn.com/images/eoveol/post/e71145eb-6bbe-4e9c-a0cc-fbfb6eb389dc/image.png)

https://velog.io/@eoveol/Algorithm-%EC%8A%A4%ED%83%9D-1

## Java Stack Class

https://docs.oracle.com/javase/8/docs/api/java/util/Stack.html

`java.util.Stack<E>`

- Stack 클래스는 객체의 LIFO(후입선출) 스택을 나타냄
- Vactor 클래스 상속

`A more complete and consistent set of LIFO stack operations is provided by the Deque interface and its implementations, which should be used in preference to this class. For example:`

```java
Deque<Integer> stack = new ArrayDeque<Integer>();
```

- 하지만 java에서는 LIFO 스택구현을 다음과 같이 하는 걸 추천

### Method

- `empty()`
- `peek()`
  - 제일 위에 있는 object **제거하지 않고** 반환 
- `pop()`
  - 제일 위에 있는 object **제거** 및 반환
- `push(E item)`
  - item 추가 
- `search(Object o)`
