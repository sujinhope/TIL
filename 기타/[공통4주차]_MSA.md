# MSA

```
https://velog.io/@tedigom/MSA-%EC%A0%9C%EB%8C%80%EB%A1%9C-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0-1-MSA%EC%9D%98-%EA%B8%B0%EB%B3%B8-%EA%B0%9C%EB%85%90-3sk28yrv0e
https://wooaoe.tistory.com/57
```



[TOC]



#### MSA란?

- **Micro Service Architecture**

  "하나의 큰 어플리케이션을 여러 개의 작은 어플리케이션으로 쪼개어 변경과 조합이 가능하도록 만든 아키텍쳐"

- 작은 레고블록(Microservice)를 하나하나 붙여 어떠한 큰 결과물을 만드는 형태

<img src="https://user-images.githubusercontent.com/33229855/89859580-467b5f80-dbdc-11ea-8032-8e2f49b2bf9d.png" alt="image" style="zoom:67%;" />



##### 기존 개발 방식 - Monolithic Architecture

- 소프트웨어의 모든 구성요소가 한 프로젝트에 통합되어 있는 형태

  => 웹의 경우 WAR 파일로 빌드되어 WAS에 배포하는 형태

- Architecture가 간단하고 유지보수가 용이하기 때문에 소규모 프로젝트에서는 훨씬 합리적

- But, 일정 규모 이상의 서비스에서는 한계

  - 커지면 커질수록 영향도 파악, 전체 시스템 구조 파악에 어려움
  - 빌드 시간 및 테스트 시간, 배포 시간이 기하급수적으로 증가
  - 서비스를 부분적으로 scale-out하기가 힘듦
  - 부분 장애가 서비스 전체 장애로 이어지는 경우 발생
  - 한 프레임워크와 언어에 종속적



##### Micro Service

- Small services, each running in its own process(스스로 돌아갈 수 있는 작은 서비스)
- Independently deployable(독립적 배포 가능)
- 특징
  - 각각의 서비스는 독립적으로 배포가 가능
  - 각각의 서비스는 다른 서비스에 대한 의존성이 최소화 되어야 함
  - 각 서비스는 개별 프로세스로 구동되며, REST와 같은 가벼운 방식으로 통신되어야 함

<img src="https://user-images.githubusercontent.com/33229855/89859889-02d52580-dbdd-11ea-909e-b42d12060d80.png" alt="image" style="zoom:67%;" />



##### MSA 특징

- API를 통해서만 상호작용 가능
- 서비스의 end-point를 API형태로 외부에 노출하고 실질적 세부사항은 모두 추상화하여 내부 구현 로직, 아키텍처와 프로그래밍 언어, DB, 품질 유지 체계같은 기술적인 사항들은 API에 의해 가려진다.



##### 장점

- 서비스 별 개별 배포 가능(배포 시 전체 서비스 중단이 없음)
- 특정 서비스에 대한 확장성 용이(클라우드 사용에 적합한 아키텍처)
- 장애가 전체 서비스로 확장될 가능성이 적음



##### 단점

- 아키텍처가 복잡하기 때문에 전체 서비스가 커짐에 따라 복잡도가 기하급수적으로 늘어날 수 있음
- 서비스 간 호출 시 API를 사용하기 때문에 통신 비용이나 Latency가 그만큼 늘어나게 됨
- 서비스가 분리되어 있기 때문에 테스트와 트랜잭션의 복잡도가 증가하고 많은 자원을 필요로 함
- 데이터가 여러 서비스에 걸쳐 분산되기 때문에 한 번에 조회하기 어렵고 데이터의 정합성 또한 관리하기 어려움
- 개발 환경과 실제 운영환경을 동일하게 가져가는 것이 쉽지 않기 때문에 통합 테스트가 어렵다.





#### MicroService Architecture의 구성

<img src="C:\Users\multicampus\AppData\Roaming\Typora\typora-user-images\image-20200811142047151.png" alt="image-20200811142047151" style="zoom:67%;" />

##### 1. Inner Architecture(남색)

- 내부의 서비스를 어떻게 잘 쪼개는지에 대한 설계

- Inner Architecture는 비즈니스나 서비스, 시스템마다 표준이 없기 때문에 가장 어려운 부분

- 고려사항

  - 마이크로 서비스를 어떻게 정의할 것인가?
  - DB Access 구조를 어떻게 설계할 것인가?
  - 마이크로 서비스 내 api를 어떻게 설계할 것인가?
  - 논리적인 컴포넌트들의 layer를 어떠한 방식으로 설계할 것인가?

  

##### 2. Outer Architecture(회색)

- Gartner에서 구분한 6개 영역
  1. External Gateway
     - 전체 서비스 외부로부터 들어오는 접근을 내부 구조를 드러내지 않고 처리하기 위한 요소
     - 사용자 인증, 권한 정책관리 수행.
     - API Gateway가 가장 핵심적인 역할
     - 서버 최앞단에서 모든 APi의 호출을 받고 라우팅을 수행
  2. Service Mesh
     - 마이크로서비스 구성 요소간의 네트워크를 제어하는 역할 수행
     - 서비스 간 통신을 위해 service discovery, service routing, 트래픽 관리 및 보안 담당 요소 수행
  3. Container Management
  4. Blacking Services
  5. Telemetry
  6. CI/CD Automation





