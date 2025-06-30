---
title: JPA 성능 최적화 완전 가이드
author: 김산하
date: 2025-06-30
category: Backend
layout: post
---

## JPA 성능 최적화의 핵심

### 1. N+1 문제 해결

#### 문제 상황
```java
// 💣 N+1 쿼리가 발생하는 코드
@Entity
public class User {
    @OneToMany(mappedBy = "user", fetch = FetchType.LAZY)
    private List<Order> orders;
}

// 사용자 조회 후 주문 내역 접근
List<User> users = userRepository.findAll(); // 1번의 쿼리
users.forEach(user -> {
    user.getOrders().size(); // 각 사용자마다 N번의 쿼리 발생
});
```

#### 해결 방법

**1) Fetch Join 사용**
```java
@Query("SELECT u FROM User u JOIN FETCH u.orders")
List<User> findAllWithOrders();
```

**2) @EntityGraph 사용**
```java
@EntityGraph(attributePaths = {"orders"})
List<User> findAll();
```

**3) @BatchSize 사용**
```java
@Entity
public class User {
    @OneToMany(mappedBy = "user")
    @BatchSize(size = 10)
    private List<Order> orders;
}
```

### 2. 페이징 최적화

```java
// 올바른 페이징 쿼리
@Query(value = "SELECT u FROM User u WHERE u.status = :status",
       countQuery = "SELECT COUNT(u) FROM User u WHERE u.status = :status")
Page<User> findByStatus(@Param("status") String status, Pageable pageable);
```

### 3. 프로젝션 활용

```java
// DTO 프로젝션으로 필요한 데이터만 조회
@Query("SELECT new com.example.dto.UserSummaryDto(u.id, u.name, u.email) " +
       "FROM User u WHERE u.active = true")
List<UserSummaryDto> findUserSummaries();
```

### 성능 측정 도구

1. **Hibernate Statistics**: 실제 쿼리 개수 확인
2. **p6spy**: 실행된 SQL 로깅
3. **Spring Boot Actuator**: 메트릭 수집

이러한 최적화 기법들을 적절히 조합하면 대용량 데이터 처리 시 큰 성능 향상을 얻을 수 있습니다!
