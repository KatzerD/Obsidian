Sirve para crear un modelo común para todos las demás vistas invocadas por los métodos de este controlador

```java
@ModelAttribute("usuarios")
public List<Usuario> poblarUsuarios() {
	List<Usuario> usuarios = new ArrayList<>();
	usuarios.add(new Usuario("Enrique", "Centurion", "enrikatzer@gmail.com"));
	usuarios.add(new Usuario("Carlos", "Orrego", "mati@gmail.com"));
	usuarios.add(new Usuario("John", "Mircha", "john@gmail.com"));
	return usuarios;
}
```

[[Anotations]]