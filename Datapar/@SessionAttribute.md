Se le asigna un objeto de la sesión
``@SessionAttribute("cliente")``

Indicamos que se va a guardar en los atributos de la sesion el objeto ``cliente``, cada que se ejecuta una peticion GET se va a obtener el objeto, se guarda en los atributos de la sesion y lo pasa a la vista.

Por ultimo en un método POST, como puede ser un método ``guardar()`` se debe borrar la sesión creada con ``.setComplete()``.

```
@PostMapping("/form")
public String guardar(@Valid Cliente cliente, BindingResult result, Model model, SessionStatus status) {
	if(result.hasErrors()) {
		model.addAttribute("titulo", "Formulario de Cliente");
		return "form";
	}
	clienteDao.save(cliente);
	status.setComplete();
	return "redirect:listar";
}
```

Esta practica se utiliza por ejemplo para campos que marcamos como ``hiden`` en un formulario.