Por defecto un RequestMapping es de tipo GET, ``value`` es sinónimo de ``path``
``@RequestMapping(value="/index")`` 

``@RequestMapping(value="/index", method=RequestMethod.GET)``
``@RequestMapping(value="/index", method=RequestMethod.POST)``
etc...

``@GetMapping(value="/index")``
``@PostMapping(value="/index")``
etc...


`value` es el parámetro por defecto que necesitan estas anotaciones, asi que se puede omitir y solo asignar el valor
``@GetMapping("/index")``


Un método puede estar mapeado a mas de una ruta URL utilizando llaves ``{ }``
``@GetMapping({"/index", "/", "/home"})``


## RequestMapping en el controlador
Un controlador que tiene métodos con un RequestMapping puede indicar una dirección url previa a la carga de esos métodos, colocando la anotación sobre la clase.

```java
@RequestMapping("/app")

public class IndexController {
...
```

Esto es útil por ejemplo al crear un CRUD, donde cada metodo es una direccion url  `/listar`, `/borrar`, `/modificar`, etc.
Y se accedería mediante
`/app/listar`...
[[Anotations]]
# Tipos de Mapeo
[[@GetMapping]]
[[@PostMapping]]
[[@PutMapping]]
[[@DeleteMapping]]
