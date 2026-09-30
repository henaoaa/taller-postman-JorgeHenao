# Taller de APIs y Postman

**Estudiante:** Jorge Henao  
**Código:** _Completar con código estudiantil_  
**Asignatura:** Ingeniería de Software II — Cotecnova

## Marco conceptual

Una API (Application Programming Interface) permite que dos aplicaciones se comuniquen mediante reglas definidas. REST es un estilo para diseñar APIs web en el que la información se organiza como recursos y se accede a ellos por medio de direcciones URL usando los métodos HTTP. Por ejemplo, en una red social un usuario, una publicación y un comentario pueden ser recursos. Un **recurso** es el dato o entidad que ofrece la API; un **endpoint** es la URL concreta para interactuar con ese recurso, como `https://jsonplaceholder.typicode.com/posts/1`. Una aplicación de transporte usa APIs para consultar ubicaciones, rutas, conductores disponibles y tarifas.

Fuentes consultadas:

- [MDN: REST](https://developer.mozilla.org/en-US/docs/Glossary/REST)
- [JSONPlaceholder: guía y recursos](https://jsonplaceholder.typicode.com/)

## Métodos HTTP

| Método | Operación CRUD | Qué hace |
|---|---|---|
| `GET` | Read (leer) | Consulta un recurso o una colección sin modificarla. |
| `POST` | Create (crear) | Envía datos para crear un recurso nuevo dentro de una colección. |
| `PUT` | Update (reemplazar) | Envía la representación completa que debe quedar en un recurso. |
| `PATCH` | Update (actualizar parcialmente) | Modifica solo los campos enviados. |
| `DELETE` | Delete (eliminar) | Solicita eliminar el recurso identificado por la URL. |

Aunque ambos se usan para actualizar, `PUT` expresa reemplazo completo y `PATCH` expresa cambio parcial. La respuesta concreta depende del contrato de cada API.

Fuentes consultadas:

- [MDN: métodos HTTP](https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Methods)
- [MDN: PUT](https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Methods/PUT)
- [MDN: PATCH](https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Methods/PATCH)

## Códigos de estado

| Familia | Significado | Ejemplo |
|---|---|---|
| `1xx` | Respuesta informativa provisional mientras se procesa la solicitud. | `100 Continue` |
| `2xx` | La solicitud se completó correctamente. | `200 OK`, `201 Created` |
| `3xx` | El cliente debe seguir otra ruta o utilizar una respuesta almacenada. | `301 Moved Permanently` |
| `4xx` | La solicitud tiene un problema atribuible al cliente: URL, datos, autenticación o permisos. | `404 Not Found` |
| `5xx` | El servidor no pudo atender una solicitud que, en principio, era válida. | `500 Internal Server Error` |

Los errores `4xx` y `5xx` se separan porque orientan la corrección. Un `4xx` normalmente implica que quien consume la API debe revisar la petición: por ejemplo, puede haber pedido un recurso inexistente o enviado datos inválidos. Un `5xx` indica que el problema está en el servicio, su lógica, sus dependencias o su infraestructura; en ese caso debe intervenir el equipo que mantiene el servidor.

Fuentes consultadas:

- [MDN: códigos de estado HTTP](https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Status)
- [RFC 9110: HTTP Semantics](https://www.rfc-editor.org/rfc/rfc9110)

## Cómo reproducir este taller

1. Instalar y abrir Postman.
2. Importar `coleccion.json` mediante **Import** → **File**.
3. Abrir la colección **Taller-API**.
4. Ejecutar cada petición y revisar el código de estado, el cuerpo y las cabeceras.
5. Para revisar las verificaciones, abrir una petición y consultar **Test Results**; en versiones nuevas de Postman los scripts aparecen en **Scripts** → **Post-response**.
6. JSONPlaceholder es una API de datos de prueba: simula las operaciones de creación, actualización y eliminación; no persiste esos cambios realmente.

## Archivos de este repositorio

| Archivo o carpeta | Contenido |
|---|---|
| `README.md` | Marco conceptual, métodos HTTP, códigos de estado e instrucciones de reproducción. |
| `hallazgos.md` | Casos ejecutados, resultados, pruebas automáticas y exploraciones. |
| `conclusiones.md` | Reflexiones sobre idempotencia, cabeceras y pruebas. |
| `coleccion.json` | Colección exportada desde Postman en formato Collection v2.1. |
| `Evidencias/` | Capturas legibles de las ejecuciones y los resultados automáticos. |
