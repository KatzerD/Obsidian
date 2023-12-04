Es una anotación para declarar un componente que cuyos métodos son de tipo ``@ResponseBody``, es decir, todos sus métodos están destinados a devolver un JSON o XML

```java
package com.bolsadeideas.springboot.app.controllers;

import java.util.List;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

import com.bolsadeideas.springboot.app.models.entity.Cliente;
import com.bolsadeideas.springboot.app.service.IClienteService;

@RestController
@RequestMapping("/api")
public class ClienteRestController {

	@Autowired
	public IClienteService clienteService;
	
	@GetMapping("/listar")
	public List<Cliente> listar() {
		return clienteService.findAll();
	}
}
```