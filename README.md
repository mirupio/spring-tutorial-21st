# spring-tutorial-21st
CEOS back-end 21st spring tutorial project

# 1주차 미션
## Spring
: java 기반 백엔드 프레임워크

## Spring이 지원하는 기술들
### 1. IoC(=Inversion of Control) 제어의 역전
#### 개념
  - 개발자가 객체를 직접 **생성, 관리**하지 않고, **Spring**이 함
  이를 위해, **'Spring Container'** 존재

#### 존재 이유
  - 기존 : **개발자**가 직접 객체를 생성하고, 관리하고, 의존성을 해결 
  - IoC 적용 후 : 이 일들을 **Spring**이 맡아주기 때문에 **코드가 간결**해지고, **유지보수가 쉬워짐**

#### 구현 방식
  - **DI(=Dependency Injection) 의존성 주입**

#### 장점

1. **결합도 낮춤**
	- 객체 간의 강한 **의존성 제거** -> 코드의 **유연성, 재사용성** 높임
    ex) new를 사용하지 않고, 인터페이스 기반으로 의존성을 주입
    
2. **유지 보수 용이**
	- 객체를 변경할 때 코드 전체를 수정할 필요 없이 설정 파일(applicationContext.xml)이나 어노테이션(@Autowired, @Inject)을 수정하면 됨
    
2. **객체 생성 및 생명 주기 관리 자동화**
	- Spring이 객체를 생성하고 소멸시켜줘서, **개발자는 비즈니스 로직에 집중**할 수 있음
    
3. **테스트 용이성**
	- 실제 객체 대신 가짜(Mock) 객체 등을 활용한 **단위테스트 작성**이 쉬워짐 


### 2. AOP(=Aspect-Oriented Programming) 관점 지향 프로그래밍
#### 개념
- **핵심 로직**과 **부가 기능**을 **분리**하는 프로그래밍 방식

#### 존재 이유
- 여러 클래스에서 반복적으로 등장하는 **공통 기능을 모듈화**해서 여러 클래스에서 쉽게 **재사용**

#### 장점
1. **코드 중복 제거**

2. **유지보수성 향상**
- 공통 기능이 한 곳에 모여 있어 수정이 필요할 때 여러 곳을 수정할 필요 없음

3. **핵심 로직과 보조 기능을 분리**
- 핵심 로직을 방해하지 않으면서 부가적인 기능을 쉽게 추가 가능
ex) 로깅, 보안, 트랜잭션 처리

### 3. PSA(=Portable Service Abstraction) 휴대 가능한 서비스 추상화
#### 개념
- 다양한 기술 스택을 **추상화**하여 일관된 방식(**통합된 인터페이스**)으로 사용할 수 있도록 제공

#### 존재 이유
- 여러 기술의 **차이**를 개발자가 직접 처리하지 않도록 하기 위해

#### 장점
1. **기술 스택 변경 용이**
	ex) JDBC에서 JPA로 전환해도 코드를 크게 수정하지 않아도 됨
    
2. **일관된 개발 방식 제공**
	- Spring이 제공하는 공통 API를 사용
    
3. **기술 종속성 제거**
	- 특정 기술에 의존하지 않고 개발
    	ex) JDBC, Hibernate, JPA, JMS 등

## Spring Bean
#### 개념
- **Spring Container**에 의해 관리되는 객체

#### 특징
1. **Spring Container가 직접 관리**
	- **Application** 또는 **BeanFactory**가 생성, 소멸 관리

2. **Singleton 기본 적용**
	- Spring Container 내에서 하나의 Bean은 하나만 생성됨
    - 기본 설정 : @Scope("singleton"), 필요하면 변경 가능 : @Scope("prototype")

3. **Lazy Initialization 가능**
	= 필요할 때만 생성됨
    - 기본 설정 : Container가 로드될 때 Bean 미리 생성, 필요하면 변경 가능 : @Lazy -> 생성 미룸

#### 존재 이유
- 의존성 주입을 위해

#### 구현 방식
1. **어노테이션 기반**
	= @Componet 계열 어노테이션 사용
	- @Component, @Service, @Repository, @Controller 등 사용 -> 자동 Bean 등록

2. **Java Config**
	= @Bean 사용
	- @Configuration 클래스 내부에서 @Bean 메서드 사용 -> 직접 Bean 등록

### Spring Bean의 라이프사이클
#### 1. 객체 생성
- @Component, @Bean 사용
	-> Spring이 Bean을 자동 생성

#### 2. 의존성 주입
- @Autowired, @Inject, @Resource 사용
	-> 의존성 자동 주입

#### 3. 초기화
- @PostConstruct 또는 init-method 속성 사용
- InitializingBean 인터페이스 구현 -> afterPropertiesSet() 메서드 호출
	-> Bean이 생성된 후 실행할 초기화 로직을 수행

#### 4. 사용
-> Bean 사용하면서 애플리케이션이 로직 수행

#### 5. 소멸
- @PreDestroy 또는 destroy-method 속성 사용
- DisposableBean 인터페이스 구현 -> destroy() 메서드 호출
	-> 애플리케이션 종료 시, Bean이 소멸되기 전 정리할 작업 수행

## Spring annotation
#### 개념
- Java에서 메타데이터를 제공하는 특수한 형태의 마커

#### 구현 방식
- **컴포넌트 스캔** : @Controller, @Service, @Repository (는 @Component 포함) -> spring bean으로 자동 등록
  - Spring container라는 '통'에 @Controller붙은 것들을 '컨트롤러 객체'로 생성해서 넣어둠
  - Spring container라는 '통'에 @Service붙은 것들을 '서비스 객체'로 생성해서 넣어둠
  - Spring container라는 '통'에 @Repository붙은 것들을 '리포지토리 객체'로 생성해서 넣어둠 
- **자동 의존관계 설정** : 생성자에 @Autowired 붙어 있으면 spring container에 있는 객체와 연결시켜줌


## 단위 테스트와 통합 테스트
### 단위 테스트 Unit Test
#### 개념
- 애플리케이션의 **개별 모듈**(클래스, 메서드 단위)만을 테스트
- 다른 모듈과의 의존성을 제거(Mocking) 하여 독립적으로 테스트

#### 존재 이유
- **빠르고 독립적**이므로 **주요 기능 검증**하는 데 유용

### 통합 테스트 Integration Test
#### 개념
- **여러 모듈**(서비스, 컨트롤러 등)이 실제로 연동되는지 테스트
- 데이터베이스, API, 파일 시스템 등과의 실제 연동 확인

#### 존재 이유
- **실제 환경과 유사**하게 동작을 검증하는 데 필요


## 느낀점
용어 자체는 익숙해도 정확히는 알지 못했던 개념들을 꼼꼼하게 정리할 수 있어서 좋았다. 이전 프로젝트에서 스프링 기술들을 한 번 경험한 후에 개념을 정리하니까 좀 더 기억에 잘 남고 재미있었다. 기술을 알고 쓰는 것과 모르는데 무턱대고 쓰는 것은 정말 차이가 클 것이기 때문에, 이번에 이렇게 이해한 개념들을 프로젝트에서 적용해볼 생각에 조금 설렌다. 또 '존재 이유' 위주로 공부하니까 이해가 더 잘되는 것 같아서 앞으로도 이런식으로 공부해야겠다.



