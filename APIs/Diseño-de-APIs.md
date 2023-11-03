# Diseño de API's
Se diseña una interfaz a través de la cual otros developers van a estar interactuando.
Se toma perspectiva de usuario final y el objetivo tiene que resolver algun problema específico del usuario final.
El éxito de una API se mide en qué tan rapido y qué tan facil otro developer puede ponerse a usar la API. Si un dev se tarda mucho, es tiempo y trabajo que nos quitan para poder dar soporte para el uso de dicha API.


**REST:** *(REpresentational State Transfer)*
Estilo de arquitectura con una serie de principios para crear *web services*.
Tiene **Recursos**, que son elementos de información que pueden ser accedidos usando un identificador global.
Teniendo en cuenta que **Cliente/Servidor** se comunican a través de una interfaz estandar *HTTP* e intercambian interpretaciones de estos **Recursos**.
Una aplicación puede interactuar con un **Recuroso** conociendo el identificador de ese **Recuroso**  y la **Acción** requerida. Es importante que la aplicación comprenda el formato de la información devuelta (la **Representacion**), que puede ser un HTML, un XML, una img u otro contenido.

## ?  (Parameter)
Se usa para buscar o filtrar datos. 
- Filtro con valores específicos Ej 1: `GET /user?age=18&city=SFO`. 
- Filtrar por datos.  Ej 2: `GET /movies/?status=released`.
- Ordenamiento. Ej 3: `GET /movies/?sort=-release_date,updated_at`.
- Uso para búsqueda sin meter toda una query en la url. Ej 4: `GET /moviews/?q=SOME_AWASOME_QUERY_TEXT`
- Uso de **Aliases**. Son útiles cuando tenemos querys que son comúnes o muy particulares. Ej 5: `GET /movies/released`.
- Se pueden limitar los campos que se quieren obtener en la respuesta. Ej 6: `GET /movies?fields=id,directors,status`
- Uso de paginación, es para limitar el numero de resultados por petición. Coincide con la interfaz gráfica, es decir que sigue y hay previamente. Tambien se pueden usar propiedades com "offset" o "limit" 
Ej 7:
```Json
GET /movies - 200OK
{
    "status": 200,
    "results": [],
    "next": "/movies?page=4",
    "previous": null
}
```
Ej 8:
```Json
GET /movies?page=3 - 200OK
{
    "status": 200,
    "results": [],
    "total": 9454,
    "next": "/movies?page=4",
    "previous": "/movies?page=2"
}
```

## Verbos / Metodos
Son operaciónes del protocolo, o verbos. 
Es importante usar plurales en la nomenclatura.
- GET: Ej: `GET /movies`
- POST: Ej: `POST /movies`
- PUT: Ej: `PUT /movies/<id>`
- PATCH: Ej: `PATCH /movies/<id>`
- DELETE: Ej: `DELETE /movies/<id>`

No extenderse con más de dos niveles, si hay más de dos, es conveniente usar un nuevo "nodo".
- GET: Ej: `GET /team/<id>/players`
- GET: Ej: `GET /team/<id>/players/<id>`
- POST: Ej: `POST /team/<id>/players`
- PUT: Ej: `PUT /team/<id>/players/<id>`
- DELETE: Ej: `DELETE /team/<id>/players/<id>`

### Versionados
Cuando son API's públicas o la usan muchos consumidores se utilizan los versionados. Si la corrección es mínima, lo correcto es informar los cambios. Pero si son radicales, es conveniente usar **versionados**
- Ej: `GET /v1/movies`

## Estados (HTTP Status Codes)
Indica qué está pasando del lado del servidor o que sucede con la respuesta, a través de estados. Ej:
- 200 - OK
- 201 - Created
- 304 - Not Found
- 400 - Bad Request
- 401 - Unauthorized
- 403 - Forbidden
- 500 - Internal Server Error

Cuando se crea el objeto es conveniente en ocaciones regresar el objeto creado para evitar reiterar consultas sobre el mismo.
Ej:
```Json
POST /movies?page=3 - 201 Created
{
    "id": 1,
    "title": "Inception",
    "status": "released"
}
```
### Estados - Manejo de Errores
Es importante comunicar los errores para facilitar al dev que consume el servicio, un mensaje informando algun mal uso u otro mensaje, sin dar más información de la que necesita.
Ej:
```Json
POST /movies?page=3 - 401
{
    "code": 1,
    "message": "Invalid access token",
    "description": "The provided access token has expired"
}
```

## JSON First
Es posible configurar el tipo de respuesta en la url usando `GET /movies?type=json`. Lo conveniente es que sea siempre json por convención, pero existe la posibilidad de cambiar ésto agregando un parametro para solicitar la respuesta en XML o Yamel.

## Authentication and Security
No se usan sessions, ni cookies. Como mínimo hay que usar Token, hay distintos y el más popular es JWT.
### **TIPS**
- Se usa SSL, obligatorio.
- Todo se valida.
- Se puede usar cache.
- Proteccion por CSRF
- Limitar los Request
- Agregar un SDK

## Documentation
Una API bien hecha no necesita mucha documentación pero aún así es importante documentar siempre. Si se están realizando operaciónes importantes detrás, es importante hacerselo saber al cliente.


## Cabeceras
Cómo funcionan: