JpaRepository hereda de CrudRepository solo que tiene funcionalidades para paginación y ordenamiento.

Pero los tipos de datos que retorna sus funciones son de tipo Page<>.

# Paginación

En el método `listar()` del controlador agregar como parámetro
``@RequestParam(name="page", defaultValue="0") int page, ...``

Importamos de ``spring.framework.data.domain`` la clase `Pageable`