Se utiliza casi de la misma manera que [[@RequestParam]], solo que extrae los valores directamente de la ruta de la URL

# Get
```java
@GetMapping("/string/{texto}")
public String variables(@PathVariable String texto, Model model) {
	model.addAttribute("resultado", "El texto enviado es: '"+ texto + "'");
	return "variables/ver";
}

@GetMapping("/string/{texto}/{numero}")
public String variables(
		@PathVariable String texto,
		@PathVariable Integer numero,
		Model model) {
	model.addAttribute("resultado", "El texto enviado es: '"+ texto +
	"' Y el numero es '" + numero + "'");
	return "variables/ver";
}
```
No se utilizan las Query Http `...?texto=hola&...` sino el Path `/Hola/...`, para la asignación solo importa el orden

`<a th:href="@{/variables/string/} + 'Hola Enrique'"> Saludar a Enrique </a>`
`<a th:href="@{/variables/string/} + ${titulo}"> Mostrar titulo </a>`
`<a th:href="@{/variables/string/} + 'Hola Enrique' + '/' + '7'"> Saludar y numero </a>`

