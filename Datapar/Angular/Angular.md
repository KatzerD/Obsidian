
## Typescript

### Atajos

Se puede recorrer un objeto con un `for` y haciendo un mapeo de `[key, value]` de la siguiente forma
```ts
for (const [key, value] of Object.entries(parametros)) {
	urlParams = urlParams + `&${key}=${value}`;
}
```

