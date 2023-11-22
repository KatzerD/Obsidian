Se utiliza para asignar el valor de una instancia de un componente a una variable, se tienen 3 formas de hacerlo

- Por Atributo
- Por Constructor
- Por Método Setter

## Por Atributo
```java
@AutoWired
private IService service;
```

## Por Constructor
```java
private IService service;

@AutoWired
public MiConstructor(Iservice service){
	this.service = service;
}
```

## Por método Setter
```java
private IService service;

@Autowired
public void setService(IService service) {
	this.service = service;
}
```

# Muchas clases que implementan una interfaz
Cuando se crean componentes que implementan una misma interfaz, y al momento de crear una instancia de esa interfaz (Para cumplir con el desacoplamiento con la inyección de dependencias), el programa no sabrá determinar de cual de todas las clases que la implementan crear la instancia, para eso existe la Anotación [@Primary]

```java
@Service("miServicioSimple")
public class MiServicio implements IServicio{

	@Override
	public String operacion() {
		return "Ejecutando...";
	}

}
```

```java
@Service("miServicioComplejo")
@Primary
public class MiServicioComplejo implements IServicio{

	@Override
	public String operacion() {
		return "Ejecutando... más";
	}
	
}
```

```java
@AutoWired
private IService service; //Traera MiServicioComplejo
```

También existe otra Anotación para seleccionar un componente en especifico [@Qualifier], esta se utiliza acompañada del nombre que se le asigno al componente

```java
@Service("miServicioSimple")
public class MiServicio implements IServicio{

	@Override
	public String operacion() {
		return "Ejecutando...";
	}

}
```

```java
@Service("miServicioComplejo")
@Primary
public class MiServicioComplejo implements IServicio{

	@Override
	public String operacion() {
		return "Ejecutando... más";
	}
	
}
```

```java
@AutoWired
@Qualifier("miServicioSimple")
private IService service; //Traera MiServicioSimple
```


