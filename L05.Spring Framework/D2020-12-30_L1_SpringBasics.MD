

# 스프링이란 무엇인가?
자바 엔터프라이즈 개발을 <br />
편하게 해주는 <br />
오픈소스 <br />
경량급 application framework <br />

# Franework 란 무엇인가?
소프트웨어를 만드는 데 기본 골격이 되는 코드
완전한 application software가 아니다
확장해서 business needs에 맞는 완전한 application으로 완성이 요구 된다.

# Framework 종류
- Web Application Framework (Spring MVC, Struts, WebWork)
- Database Application Framework (iBatis, Hibernate, SpringDAO)
- Support Framework (Log4J, Ant, JUnit)

# Application ranework 란 무엇인가?
application 전 영역을 포괄 <br />
자바 개발의 폭 넓은 간소화 <br />

# JAVA BEAN 이란 무엇인가?
컴포넌트 기반의 소프트웨어 모델 스펙 <br />
자바 객체를 재사용 가능하게 즉, 컴포넌트화 시킬 수 있는 코딩 방침을 정의 <br />

# Enterprise JAVA BEAN 이란 무엇인가?
보안, 트랜잭션지원, 분산 컴퓨팅 등의 엔터프라이즈 어플리케이션 개발 시 필요한 다양한 서비스를 컨테이너에서 제공하며 개발자는 비지니스 로직에 전념 <br />

# Spring
EJB의 비지니스 서비스 컨테이너의 기능은 유지하되 복잡성을 상당부분 제거

# Container의 필요성
- 컴포넌트 객체의 자유로운 삽입이 가능하도록 하기 위한 호출의 독립성
- 서비스를 설정하거나 찾기 위한 일관된 방법을 제시
- 싱글톤이나 팩토리를 구현할 필요 없이 단일화된 객체에 대한 접근 방법을 제공
- 비지니스 객체에 부가적으로 필요한 각종 엔터프라이즈 서비스를 제공

# 스프링 주요 모듈
<img alt="GIF" src="https://docs.spring.io/spring-framework/docs/4.0.x/spring-framework-reference/html/images/spring-overview.png"  />

# 스프링 주요 전략
- POJO를 이용한 가볍고 비침투적 개발
- DI와 인터페이스 지향을 통한 느슨한 결합도
- Aspect와 공통 규약을 통한 선언적 프로그래밍
- Aspect와 template을 통한 반복적이고 상투적(boilerplate) 코드 제거
