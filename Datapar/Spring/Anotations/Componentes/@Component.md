Esta anotación es usada en las clases que queremos que sean nuestros Beans a ser manejados por Spring. Ayuda al control de Inyección de Dependencia. Cada clase que este anotada como un componente cumple con el patrón de diseño Singleton.

Existen variaciones del @Component que simplemente son representaciones de este mismo pero con nombres distintos. Las cuales son

- [[@Service]]
- [[@Models]]
- [[@Controller]]
- [[@Repository]]

Es buena practica anotar cada clase con la anotación que le corresponda.

Para utilizar un Componente o Bean se debe utilizar la anotación [[@AutoWired]] para enviar una instancia de la clase del componente a esa otra clase.
