Para implementar seguridad con Thymeleaf se debe incluir el namespace 
`xmlns:sec="http://www.thymeleaf.org/extras/spring-security"`

Y esto agrega ciertas funcionalidades muy útiles como:

- `sec:authorize="hasRole('ROLE_ADMIN')"` 
- `sec:authorize="isAuthenticated()"` --Para saber si hay un usuario logeado
- `sec:authentication="principal.authorities"` --Para obtener sus roles