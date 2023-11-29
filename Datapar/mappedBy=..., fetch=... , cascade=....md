Cliente
```java
//Un cliente, muchas facturas
@OneToMany(mappedBy="cliente",fetch=FetchType.LAZY, cascade=CascadeType.ALL)
private List<Factura> facturas;
```
Factura
```java
//Muchas facuras, un cliente
@ManyToOne(fetch=FetchType.LAZY)
private Cliente cliente;
```

# Fetch
El fetch es el tipo de carga que se hará con los datos en los atributos con cardinalidad.

Hay dos tipos, el `LAZY` y el `EAGER`
Para optimizar consultas es recomendable utilizar un `Join fetch` en lugar de lazy.

El mas comúnmente utilizado es el ``LAZY``, o sea carga perezosa, indica que no se cargaran o leerán todas las tablas de una relación, por ejemplo en un cliente que tiene muchas facturas, no es necesario leer y cargar todas sus facturas, cosa que con `EAGER` si se haría.

# Cascade
Indica lo que ocurre con los registros de una tabla relacionadas a un registro de otra tabla.
Las operaciones `delete` y `persist`, se van a realizar en cadena/cascada.

Tiene varios tipos
- `ALL`
- `PERSIST`
- `REMOVE`
- ...

Por ejemplo en una relación ``Cliente -> Facturas`` con un `cascade=CascadeType.ALL`, si se elimina el cliente se eliminaran también de forma automática todas sus facturas.

# MappedBy
Se utiliza en asociaciones Bidireccionales, se coloca en la relación que posea OneToMany y el nombre del atributo que hace alusión a la entidad.
```java
@OneToMany(mappedBy="cliente",...)
```
