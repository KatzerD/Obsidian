# Para que sirven
Los interceptores son útiles cuando se requiere aplicar una funcionalidad especifica para ciertas peticiones HTTP y es transversal a nuestra aplicación. Cada vez que se ejecuta un método Hendler del controlador que se encarga de manejar una petición HTTP, se carga el método, se ejecuta y se envuelve esta ejecución con algún proceso que no tiene relación directa con la Lógica de Negocio, es para dar algún tipo de soporte, por ejemplo:

- Validaciones (usuarios, datos, información)
- Registrar datos 
- Manejar transacciones SQL
- Autenticación y autorización
- Cálculos
- Sistemas de monitoreo o estadísticos

Los Interceptores se pueden ejecutar antes y/o después del método del controlador.
Estos códigos Interceptores se pueden reutilizar en varios controladores y varios métodos.

![[Pasted image 20231123075011.png]]
# Métodos de un Interceptor
Los interceptores deben implementar la interfaz HandlerInterceptor o extender de la clase abstracta HandlerInterceptorAdapter

- [[preHandler()]]
- [[postHandler()]]
- [[afterCompletion()]] 

# Ejemplo de interceptor
```java
import javax.servlet.http.HttpServletRequest;

import javax.servlet.http.HttpServletResponse;

  

import org.slf4j.Logger;

import org.slf4j.LoggerFactory;

import org.springframework.stereotype.Component;

import org.springframework.web.method.HandlerMethod;

import org.springframework.web.servlet.HandlerInterceptor;

import org.springframework.web.servlet.ModelAndView;

  

@Component("tiempoTranscurridoInterceptor")

public class TiempoTranscurridoInterceptor implements HandlerInterceptor{

  

private static final Logger logger = LoggerFactory.getLogger(TiempoTranscurridoInterceptor.class);

@Override

public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler)

throws Exception {

if(handler instanceof HandlerMethod) {

logger.info("TiempoTranscurridoInterceptor: preHandle() entrando...");

logger.info("Interceptando: " + handler);

long tiempoInicio = System.currentTimeMillis();

request.setAttribute("tiempoInicio", tiempoInicio);

Random random = new Random();

Integer demora = random.nextInt(500);

Thread.sleep(demora);

return true;

}

return false;

}

  

@Override

public void postHandle(HttpServletRequest request, HttpServletResponse response, Object handler,

ModelAndView modelAndView) throws Exception {

long tiempoFin = System.currentTimeMillis();

long tiempoInicio = (Long) request.getAttribute("tiempoInicio");

long tiempoTranscurrido = tiempoFin - tiempoInicio;

if(modelAndView != null && handler instanceof HandlerMethod) {

modelAndView.addObject("tiempoTranscurrido", tiempoTranscurrido);

}

logger.info("Tiempo transcurrido: " + tiempoTranscurrido + "ms.");

logger.info("TiempoTranscurridoInterceptor: postHandle() saliendo...");

}

}
```

