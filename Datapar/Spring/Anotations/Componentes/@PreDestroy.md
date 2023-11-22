Se utiliza para realizar ciertas acciones luego de que el componente haya sido destruido.
Los componentes tienen la característica de que son Singleton, de modo que su instancia durara todo lo que dure la aplicación levantada a menos que se le defina un Contexto.

Las acciones PreDestroy generalmente se utilizan para cerrar ciertos recursos que estaban siendo utilizados.

```java
@PreDestroy
public void destroy() {
	System.out.println("Factura destruida: ".concat(descripcion));
}
```

