Ambos, los registros (records) y las clases, son constructores de tipos en Java, pero tienen algunas diferencias clave:

1. **Sintaxis Concisa:**
    
    - **Clase:** Para crear una clase en Java, generalmente necesitas definir explícitamente los campos, crear constructores, métodos `toString()`, `equals()`, `hashCode()`, etc.
    - **Record:** Un registro (record) en Java es una forma más concisa de definir una clase que se utiliza principalmente para almacenar datos de manera inmutable. En un registro, los campos y métodos como `toString()`, `equals()`, y `hashCode()` son implícitos.
2. **Inmutabilidad por Defecto:**
    
    - **Clase:** En una clase, debes gestionar explícitamente la inmutabilidad mediante la declaración de campos como `final` y proporcionando métodos de acceso para campos privados.
    - **Record:** Los registros son inmutables por defecto, lo que significa que los campos son finales y no puedes cambiar su valor después de la creación del objeto.
3. **Generación Automática de Métodos:**
    
    - **Clase:** Debes escribir métodos como `toString()`, `equals()`, y `hashCode()` manualmente o utilizar herramientas de generación de código.
    - **Record:** Estos métodos son generados automáticamente en un registro, basándose en los campos declarados.

[[Spring Boot]]