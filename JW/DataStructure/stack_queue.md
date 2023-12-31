# Stack, Queue

## 스택의 개념

- LIFO(Last in First Out)
- 활용 예시: 함수 호출(call stack), 문자열 뒤집기, 후위 표현식, 실행 취소
- 리스트(배열), 링크드 리스트로 구현 가능
    - 리스트: 배열을 적당히 작게 잡은 다음, 확보한 공간이 다 차면 새로운 배열을 할당받아 기존의 새로운 리스트를 새 배열로 옮김
        
        이런 일이 자주 일어나면 효율을 심각하게 떨어짐
        
        긴 리스트를 관리하려면 비효율이 발생
        
    - 연결리스트로 상기 단점 해결 가능

---

## 큐의 개념

- FIFO(First in First Out)
- 활용 예시: BFS, Buffer
- 마찬가지로 배열, 링크드 리스트로 구현 가능하다
    - 배열로 구현 시 맨 앞 원소를 삭제하는 연산에서 약점이 있다 → theta(n)
    - 링크드 리스트로 구현 시 앞 혹은 맨 뒤 원소의 삽입, 삭제는 유리하지만
        
        맨 뒤 원소를 삭제하는 연산에 약점이 있다. → theta(n)
        
    - 이러한 약점을 보완할 때는 Dequeue를 사용한다.(Doubly linked list or circular array 사용)