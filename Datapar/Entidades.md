Una entidad en JPA es una clase de Java que esta vinculada a una tabla de una base de datos relacional mediante a las anotaciones.

Una entidad debe implementar la Interfaz ``Serializable`` y crearse una ``serialVersionUID``

## Anotaciones de JPA
[[@Entity]]
[[@Table]]
[[@Column]]
[[@Id]]
[[@GeneratedValue]]
[[@Temporal]]

# Ejemplo de Entidad

```java
@Entity
@Table(name="clientes")
public class Cliente implements Serializable{

	private static final long serialVersionUID = 8661384449094555735L;

	@Id
	@GeneratedValue(strategy = GenerationType.SEQUENCE)
	private Long id;
	
	private String nombre;
	private String apellido;
	private String email;
	
	@Column(name="create_at")
	@Temporal(TemporalType.DATE)
	private Date createAt;
	
	//Getters & Setters...
```

# Validaciones
[[Reglas de validación]]