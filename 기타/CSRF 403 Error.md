### CSRF 403 Error 발생 시



Spring Security 적용 시 CSRF 403 Error 가 뜨는 경우



##### CSRF

- Cross Site Request Forgery(사이트 간 요청 위조)

- 웹사이트의 취약점을 이용해서 사용자가 의도하지 않는 요청을 송신하도록 하는 공격

- Http 특성인 stateless를 악용한 공격. 세션 유지에 사용되는 쿠키 정보 등이 조건이 만족할경우 자동으로 송신되는 점을 이용하여 공격.

  ex - 특정 사용자가 A 서비스에 로그인 시 브라우저에 A 서비스의 로그인 관련 쿠키 정보가 남음. 같은 브라우저에서 악의적인 코드가 있는 B 서비스로 접속 시 B에서 A로 임의의 권한이 필요한 Request를 전송할 수 있게 된다.



##### 1. CSRF().disable()

- Spring Security 4부터는 CSRF방지 기능이 디폴트로 작동하기 때문에

  Spring Security 사용 시 Get을 제외한 Post, Put, Delete 등의 메소드를 사용할 경우 403 Forbidden 에러가 발생할 수 있다. 

  => 아래 설정으로 해결.

  ```java
  // SecurityConfig.java
  ...
      http().csrf().diable()
  ...
  ```



