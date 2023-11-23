Data Access Object es una clase de persistencia que implementa y provee una interfaz común para acceder y trabajar con los datos, independiente de las tecnologías JDBC, JPA, Hibernate, etc.

Estas clases se almacenan en el package DAO.
Una ClaseDAO debe tener su interfaz IClaseDAO.

En la interfaz se crean todos los métodos de acceso a datos que debe implementar la clase DAO.




# Anotaciones para la ClaseDAO
- [[@Repository]] es un estereotipo de Component
- [[@PersistenceContext]] es una anotación para inyectar el [[EntityManager]], por defecto utiliza la configuración para conectar con H2 Database.
- [[@Transactional]]
- [[@PrePersist]]


# Querys en la ClaseDAO
```java
public List<Cliente> findAll() {
	return em.createQuery("FROM Cliente").getResultList();
}
```