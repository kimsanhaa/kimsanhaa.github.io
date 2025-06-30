---
title: 개발 환경 설정 가이드
author: 김산하
date: 2025-06-30
category: Setup
layout: post
---

## 백엔드 개발 환경 구축하기

### 필수 도구들

#### 1. Java 개발 환경
```bash
# Java 21 설치 (macOS)
brew install openjdk@21

# JAVA_HOME 설정
echo 'export JAVA_HOME=/opt/homebrew/opt/openjdk@21' >> ~/.zshrc
```

#### 2. 데이터베이스 설정
```bash
# MySQL 설치
brew install mysql

# MySQL 시작
brew services start mysql

# Redis 설치
brew install redis
brew services start redis
```

#### 3. IDE 설정
- **IntelliJ IDEA**: 권장 IDE
- **VS Code**: 가벼운 편집용
- **필수 플러그인**: Spring Boot, JPA Buddy, Database Tools

### Docker 환경 구성

```yaml
# docker-compose.yml
version: '3.8'
services:
  mysql:
    image: mysql:8.0
    environment:
      MYSQL_ROOT_PASSWORD: password
      MYSQL_DATABASE: myapp
    ports:
      - "3306:3306"
  
  redis:
    image: redis:7
    ports:
      - "6379:6379"
```

이렇게 설정하면 일관된 개발 환경을 구축할 수 있습니다!
