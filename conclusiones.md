# Conclusiones

## Tarea 8 — Idempotencia

Un método HTTP es idempotente cuando hacer una solicitud una vez o repetir exactamente la misma solicitud varias veces tiene el mismo efecto final intencional sobre el servidor. No significa necesariamente que todas las respuestas sean iguales ni que el servidor no registre las solicitudes; significa que repetir la operación no cambia de nuevo el estado final deseado.

| Método | ¿Es idempotente? | Justificación |
|---|---|---|
| `GET` | Sí | Consulta información y no pretende modificar el recurso. |
| `POST` | No | En una API real, repetirlo puede crear más de un recurso. |
| `PUT` | Sí | Repetir el mismo reemplazo deja el recurso en el mismo estado final. |
| `PATCH` | No garantizado | Puede ser idempotente según su implementación, pero HTTP no lo garantiza. |
| `DELETE` | Sí | Tras eliminar el recurso, repetir la solicitud no debe causar una segunda eliminación. |

**Observación de mis ejecuciones:** _Ejecutar varias veces la misma solicitud PUT y luego POST en Postman; anotar aquí los códigos y cuerpos obtenidos. JSONPlaceholder simula sus cambios, por lo que esta observación debe distinguir entre la respuesta mostrada y una persistencia real._

Fuente: [MDN: idempotencia](https://developer.mozilla.org/en-US/docs/Glossary/Idempotent)

## Tarea 9 — Cabeceras de respuesta

| Cabecera | Valor visto en Postman | Significado |
|---|---|---|
| `Content-Type` | _Completar_ | Indica el formato del cuerpo de respuesta; para esta API debe corresponder a JSON. |
| `Content-Length` | _Completar o reemplazar por otra cabecera observada_ | Indica el tamaño del cuerpo de respuesta en bytes. |
| `Date` | _Completar o reemplazar por otra cabecera observada_ | Indica la fecha y hora asociada a la respuesta del servidor. |

`Content-Type` es importante al probar una API porque informa cómo debe interpretarse el cuerpo. Si se esperaba JSON y se recibe HTML, texto u otro formato, la respuesta puede ser incorrecta aunque el código de estado sea exitoso. En solicitudes que envían JSON, como POST, PUT o PATCH, también se debe indicar `Content-Type: application/json`.

Fuente: [MDN: Content-Type](https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Headers/Content-Type)

## Tarea 12 — Por qué una prueba debe fallar antes de confiar en ella

Es importante observar una prueba fallar al menos una vez porque así se verifica que realmente evalúa la condición que se quiere controlar. Si una prueba siempre aparece en verde, podría estar mal escrita, no ejecutarse o validar algo distinto a lo pensado. Cambiar temporalmente la expectativa de 200 a 201 permite comprobar que Postman detecta la diferencia.

## Reflexión final 1 — De casos de prueba a plan de pruebas

La tabla de la fase 2 ya constituye un conjunto básico de casos de prueba porque cada fila tiene una entrada, un resultado esperado y un resultado obtenido. Para ser un plan de pruebas formal necesitaría además objetivo, alcance, responsables, ambiente de pruebas, calendario, datos de prueba, prioridades, criterios de inicio y cierre, riesgos y un proceso para reportar y seguir defectos.

## Reflexión final 2 — Un 404 puede ser una buena noticia

Un 404 puede ser un resultado correcto si el caso de prueba busca comprobar que la API informa apropiadamente la ausencia de un recurso. Si se esperaba 404 y se obtuvo 404, el caso pasa. Por el contrario, un 200 puede ser un defecto cuando la especificación esperaba que la petición fallara, por ejemplo al consultar un recurso inexistente. La calidad se evalúa comparando lo observado con lo esperado, no buscando que todas las respuestas sean 200.
