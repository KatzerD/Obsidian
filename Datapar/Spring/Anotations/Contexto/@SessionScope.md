Se utiliza para marcar un objeto como una sesión, por ejemplo si se trabaja con un carro de compras o un sistema de autenticación para que sean persistentes en la sesión HTTP.

Una objeto con este Scope durara lo que dure una sesión, desde que se inicia y se finaliza cuando se cierra el navegador, ocurre un timeout o cuando se invalida la sesión.

Un componente que se quiera guardar en una sesión HTTP debe implementar la interfaz Serializable para cuestiones de transporte del objeto.

```java
@Component
@SessionScope
public class Factura implements Serializable{
	//Generar el serializable id
	private static final long serialVersionUID = ...;
	...
}
```

