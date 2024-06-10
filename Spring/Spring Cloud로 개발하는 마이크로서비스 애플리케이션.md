# Spring Cloud로 개발하는 마이크로서비스 애플리케이션

---

## Microservice와 Spring Cloud의 소개

### Cloud Native Architecture

- 확장 가능한 아키텍처
- 탄력적 아키텍처
- 장애 격리

### Cloud Native Application

- CI / CD (지속적인 통합, 배포)
  - 카나리 배포, 블루그린 배포
- DevOps
- Container 가상화
  - 기존 방식 -> 가상화 방식 -> 컨테이너 방식
  - 공통적인 라이브러리나 리소스를 공유한다
  - 적은 리소스를 사용, 가볍고 빠르게 운영가능

### 12 Factors

- BASE CODE
- DEPENDENCY ISOLATION
- CONFIGURATIONS
- LINKABLE BACKING SERVICES
- STAGES OF CREATION
- STATELESS PROCESSES
- PORT BINDING
- CONCURRENCY
- DISPOSABILITY
- DEVELOPMENT & PRODUCTION PAIRTY
- LOGS
- ADMIN PROCESSES FOR EVENTURL PROCESSES
- +3
  - API FIRST
  - TELEMETRY
  - AUTHENTICATION AND AUTHORIZTAION

### Monolithic vs. Microservice

### Microservice Architecture란?

- Microservice의 특징
  - Challenges
  - Small Well Chosen Deployable Units
  - Bounded Context
  - RESTful
  - Configuration Management
  - Cloud Enabled
  - Dynamic Scale Up And Scale Down
  - CI / CD
  - Visivility

### SOA vs. MSA

- SOA - 재사용을 통한 비용 절감
  - 기술방식 : 공통의 서비스를 ESB에 모아 사업 측면에서 공통 서비스 형식으로 서비스 제공
- MSA - 서비스 간의 결합도를 낮추어 변화에 능동적으로 대응
  - 각 독립된 서비스가 노출된 REST API를 사용

### Microservice Architecture Structures

### Spring Cloud란?

---

## Service Discovery

### Spring Cloud Netflix Eureka

서비스 디스커버리란?

- 외부의 다른 서비스들이 마이크로 서비스를 검색하기 위해 사용되는 개념

- 전화번호부 같은 개념

- key, value

- 등록, 검색

- Client <-> Load Balancer, API Gatewat <-> Spring Discovery <-> Service Instance

  

---

### User Service - 등록

- Run/Debug Configurations에서 VM options을 `-Dserver.port=9002`로 하면 application.yml의 server.port를 하드코딩 할 필요가 없다

- `mvn spring-boot:run -Dspring-boot.run.jvmArguments='-Dserver.port=9003'` 
  - `spring-boot:run` - 현재 디렉토리의 스프링 부트 프로젝트를 실행
- `mvn compile package` 이후  `java -jar -Dserver.port=9004 ./target/user-service-0.0.1-SNAPSHOT.jar`

---

### API Gatewat Service

- 인증 및 권한 부여
- 서비스 검색 통합
- 응답 캐싱
- 정책, 회로 차단기 및 QoS 다시 시도
- 속도 제한
- 부하 분산
- 로깅, 추적, 상관 관계
- 헤더, 쿼리 문자열 및 청구 변환
- IP 허용 목록에 추가



