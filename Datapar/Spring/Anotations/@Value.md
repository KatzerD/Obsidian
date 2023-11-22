Accede al ``application.properties`` para obtener el valor de las Keys que generamos y así poder usarlas de manera global en el proyecto.

En el application.properties:
`texto.indexcontroller.index.titulo: Hola al Framework`

En el controlador
```java
@Value("${texto.indexcontroller.index.titulo}")
String tituloIndex;
```

Y ahora esa variable se puede utilizar en todo su contexto.

# Otro archivo de configuracion
Si se quiere puede utilizarse otro archivo donde guardar las variables globales que no sea el `application.properties`.

Por ejemplo, en el classpath de resources se crea el archivo `textos.properties`

Y en la raiz app crear la clase `TextosPropertiesConfig`

