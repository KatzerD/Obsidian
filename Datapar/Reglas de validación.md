En los atributos de una clase anotada como Entidad se pueden asignar ciertas reglas de validaciones, pero primeramente se debe importar una dependencia para validaciones en el ``pom.xml``.

```xml
<dependency>
	<groupId>org.springframework.boot</groupId>
	<artifactId>spring-boot-starter-validation</artifactId>
</dependency>`
```

# Anotaciones
Importar de ``javax.validation.constraints`` o ``jakarta.validation.constraint``
- [[@NotEmpty]]
- [[@NotNull]]
- [[@Email]]
- [[@Size]]

# Importante
Se debe anotar con @Valid en el argumento en el que se recibe el objeto/entidad del formulario junto con un objeto de tipo BindingResult 


```java
@PostMapping("/form")
public String guardar(@Valid Cliente cliente, BindingResult result, Model model) {
	if(result.hasErrors()) {
		model.addAttribute("titulo", "Formulario de Cliente");
		return "form";
	}
	clienteDao.save(cliente);
	return "redirect:listar";
}
```

# Personalizar mensajes de error
[[messages.properties]]