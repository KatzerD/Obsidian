Es una dependencia que se puede inyectar como parámetro a un método de alguna clase, permite mapear conjuntos clave/valor en la vista.

``` java
public String index(Model model){
	model.addAttribute("titulo //llave" , "Hola Spring Framework //valor");
}
```

Es importante que en la vista también se utilice el mismo nombre que el asignado en la llave.
``` html
<html xmlns:th"http://www.thymeleaf.org">
...
<title th:text="${titulo}"></title>
...
```
## Otras formas de mapear los datos

`(ModelMap moodel)...` Funciona de la misma manera que Modelo

``(Map<String, Object> model)`` Es propio de java.util
`map.put("titulo //llave" , "Hola Spring Framework //valor")`

Este es muy particular, ya que además de asignar los datos en la vista, también se le puede asignar la vista a cargar.
```java
public ModelAndView index(ModelAndView mv){
	mv.addObject("titulo //llave" , "Hola Spring Framework //valor");
	mv.setViewName("index");
	return mv;
}
```

