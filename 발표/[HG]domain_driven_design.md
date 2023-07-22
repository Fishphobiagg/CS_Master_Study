# 개요

MSA 설계에 대해 공부하다가 DDD를 알게됨 
DDD를 바탕으로 마이크로 서비스와 비즈니스 로직을 설계한다는데 정리해보기로 했다.

## 용어 정리

- **도메인**
  - 일반적인 요구사항, 소프트웨어로 해결하고자 하는 문제 영역
  - 기능적인 부분을 정의
- **도메인 모델**
  - 특정 도메인을 개념적으로 표현한 것
- **Entity**
  - 테이블 모델, 고유 식별자를 가짐
- **Value Object**
  - 데이터 표현 모델 식별자를 가지고 있지 않고 불변 타입임
    
    ```java
    // 가변 객체 
    class Cash {
    private int dollars;
    public void mul(int factor) {
        this.dollars *= factor;
    }
    }
    ```
    
    ```java
    // 불변 객체
    class Cash {
    private final int dollars;
    public Cash mul(int factor) {
        return new Cash(this.dollars * factor);
    }
    }
    ```
- **Aggregate**
  - 연관된 엔티티와 벨류 오브젝트의 묶음, 일관성과 트랜잭션, 분산의 단위
  - 데이터 변경 단위(데이터 라이프 사이클) 같은 데이터를 묶은 집합
  - root Aggregate
    - Aggregate가 제공해야 할 핵심 도메인 기능을 보유하고 있는 모델
      ![](https://velog.velcdn.com/images/eoveol/post/9edb3154-00b4-48d3-b892-0970bd9f6ba2/image.png)
- **Bounded Context**
  - 특정한 도메인 모델이 적용되는 제한된 영역
  - 경계 내에선 동일한 모델을 일관되게 적용
    ![](https://velog.velcdn.com/images/eoveol/post/e7bf5e13-4efc-444a-a7e8-3cd5c80de2c5/image.png)
- **Context Map**
  - 바운디드 컨텍스트 간의 관계 
    ![](https://velog.velcdn.com/images/eoveol/post/ecfc2d67-1449-448f-bb52-5ee52f7359ec/image.png)

## DDD

> 도메인주도 설계(Domain Driven Design :DDD)는 2001년에 ‘에릭 에반스’가 쓴 책 

**특징**

- 데이터 중심의 접근 법을 탈피해서 도메인의 모델과 로직에 집중해서 설계
- 보편적인 언어를 사용
  - 개발자와 도메인 전문가 간의 커뮤니케이션문제를 없애고 상호가 이해가능하게 모든 문서와 코드에 이르기까지 동일한 표현과 단어로 단일화된 언어체계를 구축
    (유비쿼터스 언어, 보편적 언어 사용)
- 소프트웨어 엔티티와 도메인 컨셉을 가능한 가장 가까이 일치시킴

**데이터 주도 설계란?**

- 객체가 가져야 할 데이터에 초점을 두고 설계하는 것
- 객체 자신이 포함하고 있는 데이터를 조작하는 데 필요한 행동을 정의함
  
  ```java
  public class Movie {
    private String title;
    private Duration runningTime;
    private Money fee;
    private List<DiscountCondition> discountConditions;
    private MovieType movieType;
    private Money discountAmount;
    private double discountPercent;
    // getter, setter..
  }
  ```
- 객체가 어떤 곳에서 사용될지 알 수가 없기 때문에 최대한 많은 접근자와 수정자를 만들게 됨
  -> 외부에 대부분의 구현이 노출 
  -> 캡슐화의 원칙 위배("데이터를 묻지 말고, 기능을 실행해달라고 요청")

## 도메인 주도 설계와 마이크로서비스

- MSA 설계의 주요한 가이드가 됨
  - 마이크로서비스의 어플리케이션 개발 측면
  - 응집성이 있는 도메인 중심의 마이크로서비스를 도출하는 지침
  - 마이크로서비스 내부의 비지니스 로직 설계

즉, 마이크로서비스를 도출하고 내부구조를 설계하는데 도메인 주도 설계 기법을 활용하는 것이 효과적임

## 카카오의 DDD

[카카오 Domain Driven Design 적용사례 공유](https://www.youtube.com/watch?v=4QHvTeeTsj0)

#### 배경

파트너 사이트는 카카오 페이지 앱에서 제공되는 모든 컨텐츠 관리 및 그에 따른 기능 제공함
-> 많은 Contents Provider들이 직접 파트너 사이트를 이용해 컨텐츠 생성, 업로드 등 진행, 작품에 대한 메타 정보, 판매 상태 등 관리함 또한 정산, 판매상품 통계정보 조회 가능 

기존 파트너 사이트 모놀리식하게 구성되어 있었음
-> 기술부채
-> 유지보수 어려움
-> 리소스 관리 등 어려움
-> **MSA 전환 고려**

#### 왜 하필 DDD?

테스트 중심의 TDD
행위 중심의 BDD 
도 있는데 왜 DDD?

파트너 사이트는 레거시 서버
-> 이미 큰틀과 검증된 플로우가 존재함
-> 따라서 전체적으로 한번에 갈아 엎는 빅뱅 방식 대신 필요한 기능 등을 구분하고 조금 씩 필터링 하는 점진적 향상을 선택했기 때문!
-> 레거시와 신규 서버를 동시 가동하게 함

#### DDD를 구현하기 위한 선행작업

1. **Bounded Context**
   ![](https://velog.velcdn.com/images/eoveol/post/63510032-7c20-4e0a-886d-0e122b15fa94/image.png)
   
   - 각 기능을 의존성을 줄이기 위해 분리하여 일종의 경계를 구성
     -> 이것을 토대로 MSA상 각각의 서비스로 구현!
     -> 서로 데이터의 조회 등을 위해서는 api를 사용해 통신
     -> 각 도메인 철저히 분리

2. **Context Map**
   ![](https://velog.velcdn.com/images/eoveol/post/8783ba63-74c6-4b22-84b5-d46a47560129/image.png)
- 바운디드 컨텍스트들의 관계를 보여줌
- 전체적인 흐름을 예상할 수 있게함
- 이걸 가지고 구현할 때 서비스가 가지고 있는 객체를 그대로 구현하는건 의미가 없음
- 각 도메인 영역을 대표하는 도메인 객체들의 집합을 설계 -> 어그리게이트
3. **Aggregate**
   ![](https://velog.velcdn.com/images/eoveol/post/61c321ec-46bb-4812-9041-25c0c8e7e797/image.png)
- 데이터의 변경단위
- 어그리게이트에 대한 접근은 루트 엔티티를 통해서만 가능
- 이렇게 객체들을 서로 상호작용하게 하는게 아니라 루트엔티티를 통해서만 상호작용하게 하면 객체들간의 관계를 좀 더 넓은 시야로 볼 수 있음
- 제약사항을 하나의 맥락으로 관리, 어그리게이트 관계를 봄으로써 비즈니스 로직에 집중 가능
  ![](https://velog.velcdn.com/images/eoveol/post/1df52d83-e8e0-422a-9fad-ae8771970b2b/image.png)

#### 아키텍처

DDD 대표적인 아키텍처 3가지 

- Layered
- Clean
- Hexagonal

##### Layered

<img src="https://velog.velcdn.com/images/eoveol/post/d551409b-47b6-4377-9ae7-f178c65ad0a3/image.png" title="" alt="" width="220">

- User Interface 
- Application
- Domain
- Infrastructure

##### Clean

<img src="https://velog.velcdn.com/images/eoveol/post/37766de0-86a4-47a7-b90c-6ac4522259c4/image.png" title="" alt="" width="303">

- External Interface
- Interface Adapter
- Use Case
- Entity

##### Hexagonal

<img src="https://velog.velcdn.com/images/eoveol/post/a7c3d28a-5b59-446e-9f82-6930504ff685/image.png" title="" alt="" width="434">

- 각 포트에 맞게 구현만 해주면 어떤 유틸리티든 사용가능 

##### 결론

- Layered -> 비즈니스 로직이 거대해지면서 레이어가 오염될 것을 염려해서 제외
- Clean보다 Port and Adapter라는 명확한 구현개념이 있는 Hexagoanl 선택

<img src="https://velog.velcdn.com/images/eoveol/post/24c395cf-f9a0-4be7-ad0f-a3bc8efcf2f2/image.png" title="" alt="" width="441">

#### 은총알은 없다

장점만큼 단점도 있음
**단점**

1. MSA에서 오는 단점
   - 복잡해진 개발 난이도
   - 서버들이 나눠져서 트랜잭션 관리 어려워진 통합테스트, 배포
2. 아키텍처 
   - mapper와 같은 도메인이 사용하기 위해 별도로 구현되어어지는 코드들
3. 도메인
   - 도메인에 대한 높은 이해도 필요 -> 시간 많이듬

**장점**

1. 빠른 커뮤니케이션 (기존엔 데이터 용어, 실제 서비스 용어간 차이가 있었음)
2. 복잡했던 도메인 관계 정리가능
3. 도메인 분리에 따른 유지보수 편의성
4. 새로운 기능 및 요구사항에 대한 유연성
5. Aggregate 사용으로 인해 자연스럽게 캡슐화
6. 의존도 떨어짐(유즈케이스, 포트 등 사용), 응집도는 높아짐(도메인 로직을 필요한 곳에 모아버림)
7. 코드 가독성 증가

## 출처 및 참고

https://incheol-jung.gitbook.io/docs/q-and-a/architecture/ddd
[NHN](https://www.youtube.com/watch?v=6w7SQ_1aJ0A)
[카카오 Domain Driven Design 적용사례 공유](https://www.youtube.com/watch?v=4QHvTeeTsj0)
