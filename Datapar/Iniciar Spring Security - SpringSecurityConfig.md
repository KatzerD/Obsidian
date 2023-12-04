Lo primero para utilizar Spring Security es importar las dependencias necesarias en el `pom.xml`.
Estas dependencias varían de versión a versión.

Para Spring Boot 3 con Java 17 es necesario utilizar Spring Boot 5 o 6, también se puede agregar Spring Security en el Spring Initializr e importara todas las dependencias necesarias.

```xml
<dependency>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-security</artifactId>
</dependency>
<dependency>
		<groupId>org.thymeleaf.extras</groupId>
		<artifactId>thymeleaf-extras-springsecurity6</artifactId>
</dependency>
```

Luego, en la carpeta raíz `.app` se debe crear una clase llamada `SpringSecurityConfig`.
El contenido y manera de configurar esta clase también varia de versión en versión.

Para Spring Boot 3 con Spring Security 6 es el siguiente:

```java 
package com.bolsadeideas.springboot.app;

import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.security.config.annotation.web.builders.HttpSecurity;
import org.springframework.security.core.userdetails.User;
import org.springframework.security.core.userdetails.UserDetailsService;
import org.springframework.security.crypto.bcrypt.BCryptPasswordEncoder;
import org.springframework.security.provisioning.InMemoryUserDetailsManager;
import org.springframework.security.web.SecurityFilterChain;
import org.springframework.security.web.util.matcher.AntPathRequestMatcher;

@Configuration 
public class SpringSecurityConfig { /*Otras versiones mas antiguas requieren extender de otra clase*/

	@Bean
	/*Creamos un metodo passwordEncoder().
	Este es el codificador de las contraseñas, las encrypta*/
	public static BCryptPasswordEncoder passwordEncoder() {
		return new BCryptPasswordEncoder();
	}
	
	@Bean
	/*En esta clase podemos definir y crear los usuarios y contraseñas, es autenticacion*/
	public UserDetailsService userDetailsService() throws Exception {
		
		InMemoryUserDetailsManager manager = new InMemoryUserDetailsManager();

		manager.createUser(
					User.withUsername("user").password(passwordEncoder()
							.encode("user")).roles("USER").build()
				);

		manager.createUser(
					User.withUsername("admin").password(passwordEncoder()
							.encode("admin")).roles("ADMIN", "USER").build());

		return manager;
	}

	@Bean
	/*En esta parte definimos los permisos y acceso a los recursos, es la autorizacion*/
	public SecurityFilterChain filterChain(HttpSecurity http) throws Exception {
	
		http.authorizeHttpRequests((authz) -> {
			try {
                authz
                        .requestMatchers(new AntPathRequestMatcher("/"),
                                new AntPathRequestMatcher("/css/**"),
                                new AntPathRequestMatcher("/js/**"),
                                new AntPathRequestMatcher("/images/**"),
                                new AntPathRequestMatcher("/listar/**"))
                        .permitAll()
                        .requestMatchers(
                                new AntPathRequestMatcher("/ver/**"))
                        .hasAnyRole("USER")
                        .requestMatchers(
                                new AntPathRequestMatcher("/uploads/**"))
                        .hasAnyRole("USER")
                        .requestMatchers(
                                new AntPathRequestMatcher("/form/**"))
                        .hasAnyRole("ADMIN")
                        .requestMatchers(
                                new AntPathRequestMatcher("/eliminar/**"))
                        .hasAnyRole("ADMIN")
                        .requestMatchers(
                                new AntPathRequestMatcher("/factura/**"))
                        .hasAnyRole("ADMIN")
                        .anyRequest().authenticated()
                        .and()
						//Spring Security posee un formulario de login predeterminado
                        .formLogin(login -> login.permitAll())
                        .logout(logout -> logout.permitAll());
                        
			}catch(Exception e) {
				e.printStackTrace();
			}
		});
		
		return http.build();
	}

}

```

# Formulario Login

Spring Boot tiene un Login por defecto que podemos cambiar o estilizar
```html

<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">
    <meta name="description" content="">
    <meta name="author" content="">
    <title>Please sign in</title>
    <link href="https://maxcdn.bootstrapcdn.com/bootstrap/4.0.0-beta/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-/Y6pD6FV/Vv2HJnA6t+vslU6fwYXjCFtcEpHbNJ0lyAFsXTsjBbfaDjzALeQsN6M" crossorigin="anonymous">
    <link href="https://getbootstrap.com/docs/4.0/examples/signin/signin.css" rel="stylesheet" crossorigin="anonymous"/>
  </head>
  <body>
     <div class="container">
      <form class="form-signin" method="post" action="/login">
        <h2 class="form-signin-heading">Please sign in</h2>
        <p>
          <label for="username" class="sr-only">Username</label>
          <input type="text" id="username" name="username" class="form-control" placeholder="Username" required autofocus>
        </p>
        <p>
          <label for="password" class="sr-only">Password</label>
          <input type="password" id="password" name="password" class="form-control" placeholder="Password" required>
        </p>
<input name="_csrf" type="hidden" value="fpNkSPiKKwnvMyosWE5Vah_fejNf4VjfsKIEF2gyg1ghEv-dS_YHKcm6GzjCUBtPa2NhWSbnV1Fu2Wry1JA9JV4B4WgXK878" />
        <button class="btn btn-lg btn-primary btn-block" type="submit">Sign in</button>
      </form>
</div>
</body>
</html>
```

Algo muy importante que implementa Spring Security es la protección CSRF indicada en el input 
```html
<input name="_csrf" type="hidden" value="fpNkSPiKKwnvMyosWE5Vah_fejNf4VjfsKIEF2gyg1ghEv-dS_YHKcm6GzjCUBtPa2NhWSbnV1Fu2Wry1JA9JV4B4WgXK878" />
```
con `name="_csrf"`.
Que significa Cross Site Request Forgery (Falsificación de Peticiones en Sitios Cruzados) es un tipo de exploit malicioso que pueden ejecutar vía comandos no autorizados que son transmitidos por un usuario en el cual el sitio web confía, en nuestra aplicación con esta configuración las evitamos.

Spring Security ya maneja de manera automática la protección contra CSRF, por lo que si creamos un formulario de Login nuevo este ya tendrá el input de tipo hidden con el nombre y valor del`` _csrf``, pero se puede agregar de forma manual con Thymelyef 
	`<input type="hidden" name="${_csrf.parameterName}" value="${_csrf-token}" />`

# Thymeleaf Security
[[Thymeleaf security]]

# Anotaciones
[[@EnableMethodSecurity()]]