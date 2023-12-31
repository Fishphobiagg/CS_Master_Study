# 리스트(배열 vs 링크드리스트)


## 리스트란

> 리스트는 줄 세워져 있는 데이터를 의미한다.
> 
- 인덱스를 통해 원소에 접근, 삽입, 삭제 등의 연산을 할 수 있는 **추상 데이터 타입**이다.
- 파이썬의 경우 리스트의 하부는 배열로 구현되어 있다.
- 배열과 달리 리스트는 크기가 정해져 있지 않다.

---

## 배열

- 메모리의 저장 시작 위치부터 자료를 순서대로 연속하여 저장
- 장점
    - index를 통해 빠르게 원소에 접근이 가능하다.
- 단점
    - 원소 삽입 시 오른쪽의 원소들을 한 칸씩 시프트 해야 하는 부담이 있다.
    - 배열은 공간의 크기를 미리 정해서 받아야 하는데 공간이 꽉 차있는 경우
        
        기존의 내용을 복사하여 새 배열에 매핑 해야 한다. → Overhead가 크다
        


---

## 연결 리스트


- 연결 리스트는 배열의 공간 낭비를 피할 수 있는 자료구조이다.
- 원소가 추가될 때마다 공간을 할당 받아 추가하는 동적 할당 방식을 따른다.
- 직전 노드, 직후 노드를 저장하는 레퍼런스를 사용하여 노드를 연결한다.
    - 배열과는 달리 메모리 상에 순차적으로 데이터가 위치하지 않는다.
- 장점
    - 동적으로 크기를 설정할 수 있다.
    - 삽입, 삭제가 용이하다.
- 단점
    - 임의로 액세스를 할 수 없다.
    - 레퍼런스에 대한 Overhead가 존재한다.

---

## 배열 리스트와 연결 리스트의 비교

- 배열 리스트는 연속된 공간에 원소를 저장하지만 연결 리스트는 공간의 연속성이 없다.
    - 정렬, 검색 작업을 할 때 연결 리스트에서 시간이 더 걸린다.
    - i번 원소에 접근할 때 연결 리스트에서 시간이 더 걸린다.
- 연결 리스트에는 다음 원소의 링크를 위한 공간이 추가로 필요하다.
    - 다만 배열 리스트는 공간이 부족할 경우 새로운 배열을 선언하고 기존 값을 복사해야 하는 Overhead가 커질 수 있다.

### 응용

- 원형 연결 리스트
    

    
    - 연결 리스트의 경우 첫 노드와 마지막 노드에 대한 접근성의 차이가 크다.
    - 마지막 노드가 첫 번째 노드를 링크하도록 바꾸면 맨 끝 노드의 삽입 삭제 연산을 개선 가능.

- 양방향 연결 리스트
    - 양 방향으로 연결 되어 앞 뒤로 이동 가능하다.

---