Se utiliza dentro de una clase con anotación de [[@Configuration]], se utiliza para guardar componentes en el container y crear instancias para ser inyectadas.

Los @Bean tambien pueden utilizar la anotación [[@AutoWired]] con @Primary y @Qualifier.

```java
@Configuration
public class AppConfig{
	
	@Bean("miServicioSimple")
	@Primary
	public IServicio registrarMiServicio(){
		return new MiServicio();
	}

	@Bean("miServicioComplejo")
	public IServicio registrarMiServicioComplejo(){
		return new MiServicioComplejo();
	}
}
```