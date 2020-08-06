# 공통 4주차_War, Jar



#### War, Jar

- Java의 jar 툴을 이용해서 생성된 압축 파일, 어플리케이션을 쉽게 배포하고 동작시킬 수 있도록 관련 파일(리소스, 속성 파일 등)들을 패키징해줌.

- ##### War(web Application Archive)

  - servlet/jsp 컨테이너에 배치할 수 있는 웹 어플리케이션 압축 파일 포맷
  - JSP, SERVLET, JAR, CLASS, XML, HTML, JAVASCRIPT 등 Servlet Context 관련 파일들로 패키징 되어 있음.
  - 웹 응용 프로그램을 위한 포맷이기 때문에 **웹 관련 자원만 포함**하고 있으며 이를 사용하여 웹 어플리캐이션을 **쉽게 배포하고 테스트**할 수 있다.
  - JAR와 달리 원하는 구성을 할 수 없기 때문에 WEB-INF나 META-INF 디렉토리로 **사전 정의된 구조**를 사용하며 WAR 파일을 실행하기 위해 **Tomcat, Weblogic, Websphere** 등의 웹 서버(WEB) 또는 웹 컨테이너(WAS)가 필요하다.



- ##### JAR(Java Archive)

  - Class와 같은 Java 리소스와 속성파일, 라이브러리 및 액세서리 파일이 포함됨.
  - **Java 어플리케이션이 동작할 수 있도록 자바 프로젝트를 압축한 파일**
  - 원하는 구조로 구성이 가능하며 JDK에 포함하고 있는 JRE만 가지고도 실행이 가능하다.



- ##### EAR(Enterprise Archive)

  - JAVA EE(Enterprise Edition)에서 쓰이는 파일 형식으로 한 개 이상의 모듈을 단일 아카이브로 패키징하여 어플리케이션 서버에 동시에 일관적으로 올리기 위해 사용되는 포맷

    

<img src="https://user-images.githubusercontent.com/33229855/88519039-6e8b9000-d02c-11ea-8bde-30bbb644db2e.png" alt="image" style="zoom:47%;" />