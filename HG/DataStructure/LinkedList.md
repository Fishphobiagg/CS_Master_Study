# Linked List

![](https://www.nextree.co.kr/content/images/2021/01/jdchoi_20140220_JCF.png)

- JCF계층 구조를 보면 LinkedList는 ArrayList와 달리 List 인터페이스를 구현한 AbstractList를 상속하지 않고 AbstractSequentialList를 상속함

<img src="https://velog.velcdn.com/images/eoveol/post/43f0614c-4a03-422f-8afd-1d57021641de/image.png" title="" alt="" data-align="inline">

- ArrayList는 순서대로 쭉늘어선 배열의 형식 
- LinkedList는 자료의 주소값으로 서로 연결되어 있는 구조 

## LinkedList의 장점

- 몇 개의 참조자만 바꿈으로써 새로운 자료의 삽입이나 기존 자료의 삭제를 위치에 관계없이 빠른 시간안에 수행 
  
  - ArrayList는 O(N)만큼의 연산 속도가 걸리기 때문에 자료의 최대 개수에 영향을 받음 
  - LinkedList는 자료의 개수에 영향을 받지 않음 

- LinkedList는 메모리의 용량이 충분하다면 크기가 한정되어있지 않음 
  
  - ArrayList는 크기가 한정되어 있음 
  - ArrayList의 크기를 재조정하는 연산을 수행하여 크기를 늘릴 순 있지만, 연산량이 상당함 

## 삽입/삭제 과정

### ArrayList

**삽입**
![](https://velog.velcdn.com/images/eoveol/post/915a575b-d466-4e20-9781-3609ae244526/image.png)

- 사이즈가 고정되어 있기 떄문에 사이즈를 늘려주는 연산이 있음 
  **삭제**
  ![](https://velog.velcdn.com/images/eoveol/post/e2b96cd9-2316-413b-a5d6-8823f77fa631/image.png)
- 순차적인 인덱스 구조로 인해서 삭제된 빈 인덱스를 채워야하기 때문에 채워주는 연산이 추가 되어있음 
- 지속적으로 삭제되면 그 공간 만큼 낭비되는 메모리가 많아짐 

### LinkedList

**삽입**
![](https://velog.velcdn.com/images/eoveol/post/5c23449b-42fa-4c29-b43c-fd407cc669d0/image.png)

**삭제**
![](https://velog.velcdn.com/images/eoveol/post/4683223a-e316-4d5d-a217-48c6688ed890/image.png)

- 연결형태로 삽입 삭제시 크기를 키우거나 뒤로 밀거나 채우는 작업없이 단지 주소만 서로 연결시켜 주면 되기 때문에 추가/삭제가 ArrayList보다 빠르고 용이함 

## LinkedList의 단점

- ArrayList에서는 무작위 접근이 가능하지만, LinkedList에서는 순차접근만이 가능 
- 단순 LinkedList는 단방향성을 갖고 있기 때문에 인덱스를 이용하여 자료를 검색하는 애플리케이션에는 적합하지 않음 
- 순차접근도 ArrayList가 훨씬 빠름 
  - ArrayList는 자료들을 하나의 연속적인 묶음으로 묶어 자료를 저장 
  - LinkedList는 자료들을 저장 공간에 불연속적인 단위로 저장 
    -> 메모리 이곳저곳에 산재해 저장되어 있는 노드들을 접근함 
- 참초자를 위한 추가적인 메모리 할당이 필요함 
  - 자료들의 크기가 작은 리스트의 경우 참조자를 위한 추가적인 메모리할당은 비실용적 
