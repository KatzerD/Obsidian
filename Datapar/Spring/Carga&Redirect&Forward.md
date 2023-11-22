Existen 3 formas de renderizar una pagina en Spring

# Carga
Cargando una vista HTML del template, desde el controlador
`return "index"`

# Redirect
Redireccionando a una vista o pagina externa, conservando la dirección URL de esa pagina o vista.
`return "redirec:app/index"`

# Forward
Es como redirec, carga una pagina o vista del proyecto pero no muestra la URL de la vista cargada, mantiene la que ya tiene. Por detrás lo que hace es ejecutar un `RequestDispatcher.forward()` del API Servlet.
`return "forward:/app/index";`