
En un un método en el controlador se puede asignar una variable con una anotación @RequestParam para capturar y asignar el valor de la variable indicada implícita o explícitamente en la URL
# Get
```java
@GetMapping("/string")
public String param(@RequestParam(name="textoUrl") String texto, Model model) {
	
	model.addAttribute("resultado", "El texto enviado es: " + texto);
	return "params/ver";
	
}
```
De esta forma se hace un GET. También se puede asignar un valor por defecto `defaultValue` y si el campo es requerido o no `required` en el @RequesParam. Se puede recibir mas de un parámetro concatenando varios @RequestParam.

```html
<a th:href="@{/params/string(textoUrl='Hola Enrique')}"> Saludar a Enrique </a>
```
Con Thymeleaf se puede enviar parámetros de esta forma, también se puede enviar mas de un parámetro concatenando con comas.

## Diferencia con HttpServletRequest
Misma función, diferentes códigos

```java
@GetMapping("/mix-params")
public String param(
		@RequestParam(required=false) String saludo,
		@RequestParam(required=false) Integer numero,
		Model model) {
	
	model.addAttribute("resultado", "El saludo enviado es: '" + saludo + 
		"' Y el numero es '"+numero+"'");
	model.addAttribute("titulo", "Recibir parametros del Request HTTP GET");
	return "params/ver";
}

@GetMapping("/mix-params-httpServlet")
public String param(	
		HttpServletRequest request,
		Model model) {
		
	String saludo = request.getParameter("saludo");
	Integer numero = null;
	
	try {
		numero = Integer.parseInt(request.getParameter("numero"));
	}catch(NumberFormatException e) {
		numero = 0;
	}
	
	model.addAttribute("resultado", "El saludo enviado es: '" + saludo + 
		"' Y el numero es '"+numero+"'");
	model.addAttribute("titulo", "Recibir parametros del Request HTTP GET");
	
	return "params/ver";
}
```

