
Nos permite deshacernos de la `constructor()` y para evitar situaciones, cuando intentamos usar campos antes de que se declaren (campos, declarados en el archivo `constructor()`, se inicializará después de los campos, declarados en el cuerpo de la clase). Si intentamos usar un campo que aún no está inicializado, TypeScript generará un error:

```ts
export class ExampleComponent {  
	private readonly profile$ = this.authService.getCurrentUserProfile();  
	// ‼️ TS2729: Property authService is used before its initialization.  
	private readonly authService = inject(AuthenticationService);
}
```
Y si el authService lo declaramos en el constructor, si se podra compilar pero dara un error en tiempo de ejecucion.

```ts
//Component
`@Component({  
	selector: 'app-example',  
	template: 
`})
export class ExampleComponent {  
	private readonly authService = inject(AuthenticationService);  
}  

//Service
@Injectable({ providedIn: "root" })  
class AuthenticationService {  
	private readonly http = inject(HttpClient);   
	
	getCurrentUserProfile(): Observable<UserProfile> {  
		return this.http.get<UserProfile>('/user/profile');  
	}  
}
```
De esta forma se puede utilizar el metodo `inject()`

In that decorator, you can define if you want a “singleton” or not, using `providedIn`. Initially, it had multiple possible options, but they all deprecated, and there is just one choice you can make: add `providedIn: "root"` or not.

It is very convenient, but you should not forget one thing: singletons (`providedIn: “root”`) share a single instance with all the consumers. And every internal variable of your service can be modified by multiple components.

We can modify the strategy of `inject()` a little, using the second argument, that accepts `InjectOptions`:

```ts
interface InjectOptions {  
  // Use optional injection, and return null if the requested token   
  // is not found.  
  optional?: boolean;  
  // Start injection at the parent of the current injector.  
  skipSelf?: boolean;  
  // Only query the current injector for the token, and don't fall back   
  // to the parent injector if it's not found.  
  self?: boolean;  
  // Stop injection at the host component's injector.  
  host?: boolean;  
}
```

## Code Reuse
Components are difficult to reuse because they have templates. Because of that, all the code that doesn’t contain knowledge about the template details is better to move to a **_local store_** — a special service that will be instantiated together with a component, and destroyed when the component is destroyed.

If we take a look at the steps of `inject()` again (see above), we’ll find out that to get a local instance of our store, we need to:

1. Add decorator `@Injectable()` to the class of our store;
2. Do not add `providedIn: "root"`
3. Add the name of our store to the list of `providers` of our component.


[[Angular]]