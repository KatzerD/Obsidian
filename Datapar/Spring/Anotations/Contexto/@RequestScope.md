Con este tipo de Scope un objeto o componente durara lo que dure una solicitud Http, es decir una Request.
```java
@Component
@RequestScope
public class Factura{
	...
}
```
