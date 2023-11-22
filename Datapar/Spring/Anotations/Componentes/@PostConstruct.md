Se ejecuta luego del constructor de una clase, se utiliza comúnmente para inicializar ciertas cualidades del componente y hacer el código mas elegante y fácil de leer.

```java
@PostConstruct
public void init() {
	cliente.setNombre(cliente.getNombre().concat(" ").concat("Daniel"));
	descripcion = descripcion.concat(" del cliente: ").concat(cliente.getNombre());
}
```

