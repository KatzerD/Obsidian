A través del componente Object/XML (OXM) podemos mapear un objeto a un XML y viceversa.
El proceso de objeto a XML se llama ``Marshalling`` y el proceso de XML a objeto se llama ``Unmarshaller``.

La API que se utiliza para estas conversiones se obtiene a través de la siguiente dependencia:
```xml
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-oxm</artifactId>
    <version>6.0.0</version>
</dependency>
```
Para versiones de JDK 9 y superiores es necesario integrar también estas dos dependencias
```xml
		<dependency>
			<groupId>org.glassfish.jaxb</groupId>
			<artifactId>jaxb-runtime</artifactId>
		</dependency>
		<dependency>
			<groupId>javax.xml.bind</groupId>
			<artifactId>jaxb-api</artifactId>
			<version>2.3.1</version>
		</dependency>
```

# Configurar el Marshaller
En la clase `MvcConfig` agregar el ``@Bean`` **Jaxb2Marshaller**
```java
//Conversor a XML
	@Bean
	Jaxb2Marshaller jaxb2Marshaller() {
		Jaxb2Marshaller marshaller = new Jaxb2Marshaller();
		marshaller.setClassesToBeBound(new Class[] {});
	
		return marshaller;
	}
```
# Wrapper 
O envoltura en español, es una clase que envuelve una Lista/Colección para convertirla en XML
