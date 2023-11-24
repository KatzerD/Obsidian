Esta basado en el patrón de diseño Facade, un único punto de acceso hacia distintos DAO o repositorios.

Dentro de una clase Service podríamos tener como atributos y operar con diferentes clases DAO, además evitamos tener que acceder de forma directa a los DAOs dentro de los controladores.

Por cada método en la clase DAO vamos a tener métodos en el Service. Incluso en un método de la clase Service podríamos interactuar con diferentes DAOs y todo dentro de la misma transaccion.
