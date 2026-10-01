# Hallazgos de experimentación

> **Nota de trazabilidad:** los campos “código obtenido” y “¿coincide?” se deben completar al ejecutar cada petición en Postman. Los códigos esperados se registraron antes de enviar las solicitudes.

## Tabla de peticiones

| # | Petición | Código esperado | Código obtenido | ¿Coincide? |
|---|---|---:|---:|---|
| 1 | `GET /posts/1` | 200 | 200 | Sí |
| 2 | `GET /posts` | 200 | 200 | Sí |
| 3 | `GET /posts/9999` | 404 | 404 | Sí |
| 4 | `POST /posts` | 201 | 201 | Sí |
| 5 | `PUT /posts/1` | 200 | 200 | Sí |
| 6 | `PATCH /posts/1` | 200 | 200 | Sí |
| 7 | `DELETE /posts/1` | 200 | _Pendiente de ejecutar_ | _Pendiente_ |

Base URL utilizada:

```text
https://jsonplaceholder.typicode.com
```

## Tarea 4 — Recurso y colección

### `GET /posts/1`

- **URL:** `https://jsonplaceholder.typicode.com/posts/1`
- **Resultado observado:** `200 OK`.
- **Cantidad esperada:** un objeto, es decir, un recurso individual.
- **Campos esperados:** `userId`, `id`, `title` y `body`.
- **Evidencia requerida:** `Evidencias/01-get-recurso.png`.

### `GET /posts`

- **URL:** `https://jsonplaceholder.typicode.com/posts`
- **Resultado observado:** `200 OK`.
- **Cantidad esperada:** una colección de 100 publicaciones, según la documentación de JSONPlaceholder.
- **Campos por elemento esperados:** `userId`, `id`, `title` y `body`.
- **Evidencia requerida:** `Evidencias/02-get-coleccion.png`.

Un recurso individual se acepta cuando la API devuelve el objeto correcto, con sus campos y tipos esperados. Una colección requiere además verificar que el cuerpo sea un arreglo, que contenga la cantidad esperada de elementos y que cada elemento conserve la estructura acordada.

## Tarea 5 — Recurso inexistente

- **URL:** `https://jsonplaceholder.typicode.com/posts/9999`
- **Cuerpo observado:** `{}`.
- **Evidencia requerida:** `Evidencias/03-error-404.png`.

El caso de prueba pasa si se esperaba un `404` y se obtuvo un `404`: el comportamiento observado coincide con el criterio de aceptación. Un código diferente de 200 no significa por sí mismo que una prueba falló. Si la misma petición devolviera `200` con un cuerpo vacío, sería un defecto respecto al comportamiento esperado, porque informaría éxito para una consulta de un recurso inexistente.

## Tarea 6 — Creación con POST

### Configuración

- **Método:** `POST`
- **URL:** `https://jsonplaceholder.typicode.com/posts`
- **Body:** raw → JSON

```json
{
  "title": "Mi primera prueba",
  "body": "Taller de Ingeniería de Software II",
  "userId": 1
}
```

### Cinco ejecuciones

| Ejecución | ID devuelto | Código obtenido |
|---:|---:|---:|
| 1 | 101 | 201 |
| 2 | _Completar_ | _Completar_ |
| 3 | _Completar_ | _Completar_ |
| 4 | _Completar_ | _Completar_ |
| 5 | _Completar_ | _Completar_ |

**Observación:** JSONPlaceholder anuncia que simula la creación; por eso una respuesta exitosa no prueba que exista un nuevo registro persistido. En una API real comprobaría el recurso con un `GET` al ID retornado, revisaría que aparezca en la colección y, si corresponde, validaría su registro en la base de datos.

**Evidencia requerida:** `Evidencias/04-post-creacion.png`.

## Tarea 7 — Diferencia entre PUT y PATCH

### Solicitud PUT

```text
PUT https://jsonplaceholder.typicode.com/posts/1
```

```json
{
  "title": "Título corregido"
}
```

**Respuesta completa obtenida:**

```json
{
  "title": "Título corregido",
  "id": 1
}
```

### Solicitud PATCH

```text
PATCH https://jsonplaceholder.typicode.com/posts/1
```

```json
{
  "title": "Título corregido"
}
```

**Respuesta completa obtenida:**

```json
{
  "userId": 1,
  "id": 1,
  "title": "Título corregido",
  "body": "quia et suscipit\nsuscipit recusandae consequuntur expedita et cum\nreprehenderit molestiae ut ut quas totam\nnostrum rerum est autem sunt rem eveniet architecto"
}
```

**Conclusión:** `PUT` representa un reemplazo de la representación completa, mientras que `PATCH` indica una modificación parcial. Para corregir solamente un error en el título elegiría `PATCH`, pues comunica que el cambio se limita a ese campo. En JSONPlaceholder debe compararse la respuesta de ambas ejecuciones, recordando que sus cambios son simulados.

## Tarea 10 — Valores límite

| Prueba | Código obtenido | Observación |
|---|---:|---|
| `GET /posts/100` | _Completar_ | Último ID esperado dentro del rango documentado. |
| `GET /posts/101` | _Completar_ | Primer ID esperado fuera del rango. |

Este es un caso de prueba de **valores límite**. Se prueban valores en el borde de un rango válido y justo fuera de él, porque allí son frecuentes los errores de comparación y validación, por ejemplo usar `<` cuando se requería `<=`.

## Tarea 11 — Otros recursos y ruta anidada

| Ruta probada | Código obtenido | Qué se encontró |
|---|---:|---|
| `GET /users` | _Completar_ | _Completar con observación propia._ |
| `GET /todos` | _Completar_ | _Completar con observación propia._ |
| `GET /posts/1/comments` | _Completar_ | _Completar con observación propia._ |

La ruta `/posts/1/comments` expresa una relación: primero se identifica el post con ID 1 y después se solicita su colección de comentarios. También existe la consulta equivalente mediante filtro: `/comments?postId=1`.

## Tareas 12 y 13 — Pruebas automáticas

### Estado esperado

```javascript
pm.test("El estado es 200", function () {
  pm.response.to.have.status(200);
});
```

Para comprobar que la prueba funciona, se cambió temporalmente `200` por `201`; el resultado debe fallar. Después se debe restaurar `200` antes de exportar la colección.

### Campo obligatorio

```javascript
pm.test("La respuesta tiene el campo title", function () {
  const cuerpo = pm.response.json();
  pm.expect(cuerpo).to.have.property("title");
});
```

### Tipo de dato

```javascript
pm.test("El userId es de tipo número", function () {
  const cuerpo = pm.response.json();
  pm.expect(cuerpo.userId).to.be.a("number");
});
```

### Tiempo de respuesta

```javascript
pm.test("La respuesta tarda menos de 1000 ms", function () {
  pm.expect(pm.response.responseTime).to.be.below(1000);
});
```

### Tamaño de colección

> Esta prueba debe ir en `GET /posts`, no en `GET /posts/1`.

```javascript
pm.test("La colección contiene 100 publicaciones", function () {
  const posts = pm.response.json();
  pm.expect(posts).to.be.an("array");
  pm.expect(posts).to.have.lengthOf(100);
});
```

**Evidencias:** `Evidencias/05-test-automatico.png` muestra las pruebas en verde y `Evidencias/05-test-automatico-fallo.png` muestra la prueba de estado fallando temporalmente en rojo.

## Fuentes

- [JSONPlaceholder: guía oficial](https://jsonplaceholder.typicode.com/)
- [Postman Docs: ejemplos de pruebas](https://learning.postman.com/docs/tests-and-scripts/write-scripts/test-examples/)
- [MDN: idempotencia](https://developer.mozilla.org/en-US/docs/Glossary/Idempotent)
