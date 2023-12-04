Esta anotación la colocamos en los métodos de un controlador de Spring, para asignar ciertos roles de usuarios a ciertos recursos o url's.
``@Secured("ROLE_ADMIN")``
``@Secured({"ROLE_ADMIN", "ROLE_USER", ...})``
