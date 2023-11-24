CrudRepository es una interfaz propia de Spring que ya incorpora todos los métodos CRUD para poder extenderse a nuestra Interfaz DAO.

También existe una interfaz llamada JpaRepository incluye otros métodos por ejemplo para paginación y ordenamiento.

```java
public interface CrudRepository<T, ID> extends Repository<T, ID> {

  <S extends T> S save(S entity);      

  Optional<T> findById(ID primaryKey); 

  Iterable<T> findAll();               

  long count();                        

  void delete(T entity);               

  boolean existsById(ID primaryKey);   

  // … more functionality omitted.
}
```

# Consultas en JPA

Consultas por nombre del metodo.
```java
public interface UserRepository extends Repository<User, Long> {

  List<User> findByEmailAddressAndLastname(String emailAddress, String lastname);
}
```
|Keyword|Sample|JPQL snippet|
|---|---|---|
|`Distinct`|`findDistinctByLastnameAndFirstname`|`select distinct …​ where x.lastname = ?1 and x.firstname = ?2`|
|`And`|`findByLastnameAndFirstname`|`… where x.lastname = ?1 and x.firstname = ?2`|
|`Or`|`findByLastnameOrFirstname`|`… where x.lastname = ?1 or x.firstname = ?2`|
|`Is`, `Equals`|`findByFirstname`,`findByFirstnameIs`,`findByFirstnameEquals`|`… where x.firstname = ?1`|
|`Between`|`findByStartDateBetween`|`… where x.startDate between ?1 and ?2`|
|`LessThan`|`findByAgeLessThan`|`… where x.age < ?1`|
|`LessThanEqual`|`findByAgeLessThanEqual`|`… where x.age <= ?1`|
|`GreaterThan`|`findByAgeGreaterThan`|`… where x.age > ?1`|
|`GreaterThanEqual`|`findByAgeGreaterThanEqual`|`… where x.age >= ?1`|
|`After`|`findByStartDateAfter`|`… where x.startDate > ?1`|
|`Before`|`findByStartDateBefore`|`… where x.startDate < ?1`|
|`IsNull`, `Null`|`findByAge(Is)Null`|`… where x.age is null`|
|`IsNotNull`, `NotNull`|`findByAge(Is)NotNull`|`… where x.age not null`|
|`Like`|`findByFirstnameLike`|`… where x.firstname like ?1`|
|`NotLike`|`findByFirstnameNotLike`|`… where x.firstname not like ?1`|
|`StartingWith`|`findByFirstnameStartingWith`|`… where x.firstname like ?1` (parameter bound with appended `%`)|
|`EndingWith`|`findByFirstnameEndingWith`|`… where x.firstname like ?1` (parameter bound with prepended `%`)|
|`Containing`|`findByFirstnameContaining`|`… where x.firstname like ?1` (parameter bound wrapped in `%`)|
|`OrderBy`|`findByAgeOrderByLastnameDesc`|`… where x.age = ?1 order by x.lastname desc`|
|`Not`|`findByLastnameNot`|`… where x.lastname <> ?1`|
|`In`|`findByAgeIn(Collection<Age> ages)`|`… where x.age in ?1`|
|`NotIn`|`findByAgeNotIn(Collection<Age> ages)`|`… where x.age not in ?1`|
|`True`|`findByActiveTrue()`|`… where x.active = true`|
|`False`|`findByActiveFalse()`|`… where x.active = false`|
|`IgnoreCase`|`findByFirstnameIgnoreCase`|`… where UPPER(x.firstname) = UPPER(?1)`|


# Consultas por @Query
Toda la información sobre los Querys en [JPA Query Methods :: Spring Data JPA](https://docs.spring.io/spring-data/jpa/reference/jpa/query-methods.html)

```java
public interface UserRepository extends CrudRepository<User, Long> {

  @Query("select u from User u where u.emailAddress = ?1")
  User findByEmailAddress(String emailAddress);
}
```

Query nativa
```java
public interface UserRepository extends JpaRepository<User, Long> {

  @Query(value = "SELECT * FROM USERS WHERE LASTNAME = ?1",
    countQuery = "SELECT count(*) FROM USERS WHERE LASTNAME = ?1",
    nativeQuery = true)
  Page<User> findByLastname(String lastname, Pageable pageable);
  
}
```

# IMPORTANTE
La interface **PagingAndSortingRepository** ya no extiende de **CrudRepository** sino que extiende de **Repository** y no incluye los métodos del Crud.

Tenemos dos soluciones:

La primera es en vez de usar `PagingAndSortingRepository` extendemos de [[JpaRepository]]

1. public interface IClienteDao extends JpaRepository<Cliente, Long>{
2. }

Mas [detalles](https://docs.spring.io/spring-data/jpa/docs/current/api/org/springframework/data/jpa/repository/JpaRepository.html).  

La segunda solución es extender de ambas separado por coma, de `PagingAndSortingRepository` y `CrudRepository`:

1. public interface IClienteDao extends PagingAndSortingRepository<Cliente, Long>, CrudRepository<Cliente, Long>{
2. }