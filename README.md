# 스프링 시큐리티 

- 스프링 시큐리티란 스프링 기반 어플리케이션의 인증과 권한을 담당하는 스프링의 하위 프레임워크이다. 
  - 인증 : 로그인을 의미한다. 
  - 권한 : 인증된 사용자가 어떤 것을 할 수 있는지를 의미한다. 
- @Configuration : 
  - 스프링의 환경설정 파일임을 의미하는 애너테이션이다. 
- @EnableWebSecurity : 
  - 모든 요청 URL이 스프링 시큐리티의 제어를 받도록 만드는 애너테이션이다. 
  - 이 애너테이션을 사용하면 내부적으로 SpringSecurityFilterChain 이 동작하여 URL 필터가 적용된다. 
- CSRF :
  - cross site request forgery 
  - 웹사이트 취약점 공격방지를 위해 사용하는 기술 
  - 스프링 시큐리티가 CSRF 토큰 값을 세션을 통해 발행하고 웹 페이지에서는 폼 전송시에 해당 토큰을 함께 전송하여 실제 웹 페이지에서 작성된 데이터가 전달되는지를 검증하는 기술이다.
- BCryptPasswordEncoder : 
  - BCrypt 해싱 함수를 사용해서 비밀번호를 암호화한다. 
  - 직접 new 로 생성하는 방식보다는 빈으로 등록해서 사용하는 것이 좋다. 
  - 만약 암호화방식을 변경하게 되면 BCryptePasswordEncoder를 사용한 모든 프로그램을 일일이 찾아서 수정해야하기 때문이다. 
  - @Configuration이 적용된 SecurityConfig에 @Bean 메서드를 생성하는 것이다.

```java
    @Bean
    PasswordEncoder passwordEncoder() {
        return new BCryptPasswordEncoder();
    }
```

- 로그인을 수행하는 방법 : 
  - 로그인을 수행하는 방법에는 여러가지가 있다. 
  - 이 프로젝트에서는 데이터베이스에 유저의 정보를 저장했기 때문에 데이터베이스에서 유저의 정보를 조회하는 방식으로 수행할 것이다. 
  - UserSecurityService를 만들고 그 서비스를 스프링 시큐리티에 등록하는 방법에 대해서 알아볼 것이다. 
    - 이것을 위해서는 UserRepository와 UserRole 등의 준비를 먼저 해야한다. 