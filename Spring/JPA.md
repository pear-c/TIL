## 데이터베이스 정규화

- 정규화는 데이터 중복으로 인해 발생하는 데이터 불일치 현상을 해소하는 과정이다.
    
- 정규화는 주로 테이블을 더 작고, 잘 조직된 테이블로 나누는 과정이고, 나누어진 테이블 사이의 관계(relationship)를 외래 키(Foreign Key, FK)로 연결한다.
    
## 테이블 사이의 관계

- 테이블 사이의 관계(relationship)는 주로 외래 키(Foreign Key, FK)를 사용하여 한 테이블의 데이터가 다른 테이블의 데이터와 어떻게 연결되는지 정의한다.
    
- 연관된 데이터를 결합하여 조회할 필요가 있을 때, 여러 테이블 간의 관계(relationship)를 JOIN 연산을 이용하여 결합하여 조회할 수 있다.

# 관계의 종류

JPA 연관 관계는 관계의 다중성(Multiplicity)과 관계의 방향(Direction)에 의해 결정된다.

- 일대일 단방향 관계(One-to-one unidirectional association)
- 일대일 양방향 관계(One-to-one bidirectional association)
- 일대다 단방향 관계(One-to-many unidirectional association)
- 일대다 양방향 관계(One-to-many bidirectional association)
- 다대일 단방향 관계(Many-to-one unidirectional association)
- 다대일 양방향 관계(Many-to-one bidirectional association)
- 다대다 단방향 관계(Many-to-many unidirectional association)
- 다대다 양방향 관계(Many-to-many bidirectional association)

@ManyToOne(cascade = CascadeType.PERSIST, optional = false)
-> 여기서 Cascade 가 JpaRepository 메서드 기준으로 영속성 전이가 걸리는 것이 아니라,
내부 메서드에서 분기가 됨. (새거면 Persist, 아니면 merge)

## 관계 종류 특성

### 다중성
-  One-to-one (일대일, 1:1) : `@OneToOne`
- One-to-many (일대다, 1:N) : `@OneToMany
- Many-to-one (다대일, N:1) : `@ManyToOne`
- Many-to-many (다대다, M:N) : `@ManyToMany`

### 방향
- 단방향
- 양방향

### 관계의 주인
- 관계를 관리하는 책임이 있는 필드.
	- 관계를 관리한다. -> 외래 키나 조인 테이블을 관리(저장, 수정, 삭제) 한다.
- 관계의 주인인 필드가 있는 엔티티를 소유 측이라고 한다.
	- 소유 측은 보통 **외래키(FK)** 가 있는 테이블
- 소유 측의 반대쪽을 비소유 측이라고 함.
	- 양방향 관계에서 비소유 측 엔티티에는 `mappedBy` 속성을 붙여야함.
