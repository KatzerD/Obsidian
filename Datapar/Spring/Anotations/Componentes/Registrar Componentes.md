Spring posee un Container donde guarda y administra todos los componentes que hemos creado.
Spring nos provee de dos formas de registrar componentes en su contenedor:
- [[@Component]]
- [[@Bean]]

El @Component es una anotación que se utiliza en la propia clase, mientras que @Bean es se utiliza en una clase anotada con @Configuration, donde se crean instancias de todas las clases que queremos que figuren como componentes.

Tanto las clases creadas con @Component como las que son instanciadas con @Bean deben estar en la carpeta raíz del proyecto o en alguna subcarpeta de esta.

[[Ciclo de vida]]

# Cuando utilizar @Component y @Bean

Generalmente @Component se utiliza en clases que hemos creado **nosotros mismos**, mientras que @Bean se utiliza para clases creadas por **terceros**