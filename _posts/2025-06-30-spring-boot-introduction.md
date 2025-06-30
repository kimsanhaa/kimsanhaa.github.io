---
title: Spring Boot 시작하기
author: 김산하
date: 2025-06-30
category: Backend
layout: post
---

## Spring Boot란?

Spring Boot는 Java 기반의 웹 애플리케이션을 빠르게 개발할 수 있도록 도와주는 프레임워크입니다.

### 주요 특징

1. **자동 설정**: 복잡한 설정 없이 바로 시작 가능
2. **내장 서버**: Tomcat이 내장되어 있어 별도 서버 설정 불필요
3. **스타터 의존성**: 필요한 라이브러리들을 묶어서 제공

### 간단한 예제

```java
@SpringBootApplication
public class Application {
    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }
}
```

이렇게 간단하게 Spring Boot 애플리케이션을 시작할 수 있습니다!
