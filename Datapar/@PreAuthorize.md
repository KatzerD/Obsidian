Se utiliza para lo mismo que el @Secured pero con otra sintaxis

``@PreAuthorize(hasRole("ROLE_ADMIN"))``
``@PreAuthorize(hasÀnyRole({"ROLE_ADMIN", "ROLE_USER, ..."}))``