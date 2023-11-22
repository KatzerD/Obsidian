Es una clase simple que contiene atributos para sus datos y sus respectivos métodos Getters y Setters, puede implementar interfaces como serializables propias del Core de Java pero no de algún Framewok como Spring o Hibernate.

La idea es que estas clases sean completamente desacopladas de cualquier Framework o API.

Los Modelos de la capa Model deben cumplir con estos requisitos.

La nomenclatura utilizada para el paquete donde se guardan las clases POJO pueden ser
- .pojo
- .domain
- entity

[[Spring Boot]]