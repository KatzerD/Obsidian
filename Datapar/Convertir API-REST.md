Es bastante automatica.
El objetivo es implementar no una vista, sino un método Handler del controlador que se encargue de renderizar una vista del tipo REST.
Este método debe devolver un objeto, o una lista de cualquier tipo ``(List, Collection, Map, Page, etc).``

```java
	@GetMapping("/api/listar")
	@ResponseBody
	public List<Cliente> listar() {
		return clienteService.findAll();
	}
```

Para que cargue el objeto en la URL se debe agregar la anotación [[@ResponseBody]]

No olvidar agregar el nuevo Path a la configuración de seguridad.

# Controlador REST
[[@RestController]]