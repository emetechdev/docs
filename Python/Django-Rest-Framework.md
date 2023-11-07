# Conceptos Fundamentales que componen una petición en DJRestFr.

## Request
**Request** extiende de **HttpRequest** y por ende, hereda: *".data", "query_params", ".parsesrs", etc.*.
Define también atributos de la autenticación para que se pueda acceder a los datos, entre otras cosas como método, tipo de contenido, etc.

- *[modificación: Noviembre 2020]*

## Response
**Response** extiende de **HttpResponse** y hereda cosas de éste como: *"data", "status", "templed_name", "headers", "content_type"*.

Particularmente los **status** (`from rest_framework import status`) se puedde retornar alguno que ya viene definido en el framework. Ej: 
```python
return Response(content, status=status.HHTP_404_NOT_FOUND)
```
Hay varias opciones para retornar.

- *[modificación: Noviembre 2020]*

## Renderers
Así como se reciben datos de múltiples formatos, los renderers son los que devuelven los datos parseados a través de los **Serializers** y se definen por proyecto en el "config" del mismo. Por ejemplo:
```python
    REST_FRAMEWORK = {
        'DEFAULT_RENDERER_CLASSES': [
            'rest_framework.renderers.JSONRenderer',
            'rest_framework.renderers.BrowsableAPIRenderer',
        ]
    }
```
**BrowsableAPIRenderer** Lo que hace es poner una interfaz gráfica en el navegador que pinta la interfaz de la API y da las opciones de mostrarla en distintos formatos. Es muy similar a la interfaz de swagger, así que se la puede obviar

El orden en el que se agregan los renderers importa porque los toma en el orden en que aparecen. Por ejemplo, se pone primero **JSONRenderer** y después **BrowsableAPIRenderer** para que pinte primero JSON.

Se pueden agregar otros renderers como html, yml, xml, csv, excel, png u otros para devolver los datos. Hay que ver en la docu para agregarlo porque hay opciones hasta para **pandas**


- *[modificación: Noviembre 2020]*

## Parsers
La API puede recibir json, ymel, xml u otros. Entonces los **parsers** lo que hacen es validar que éstos datos que recibe estén en el formato que dicen ser, es decir, en el que están siendo enviados a través del **Header Content Type** y despúes se los pasa al elemento del request, que pueden ser el "data" o al "body params".
Entonces, cuando el **request.data** es accesado, el framework examina el **Content-type** y determina que parser va a usar para parsear el "request content"

En DJRestFr. por default el typo de contenido es **JSON** pero ésto se puede modificar, para hacerlo leer más en la docu oficial.


- *[modificación: Noviembre 2020]*

## Ahutenticación
La autenticación asocia una petición a un usuario y una vez que ésto sucede al objeto request se le asignan dos propiedades:

- request.user: Que es una instancia del "User.contrib.auth" o del que se esté usando. Es decir que **request.user** va a tener una instancia del **Modelo de Usuario**
- request.auth: Que es una variable que no tiene un formato definido pero se la puede configurar para lo que se necesite. Esta tiene información acerca de la autenticación.

Por default DJRestFr. incluye dos autenticaciónes: **SessionAuthentication y BasicAuthentication**.


- *[modificación: Noviembre 2020]*

## Permissions
Una vez que el usuario ya fué autenticado, el permiso se encarga de determinar si el usuario autenticado tiene la autorización de acceder a la vista y de que forma, es decir si es sólo lectura o si puede realizar más acciones, además de determinar el permiso por los atributos del usuario, si es "admin", si es "usuario normar", etc.

Los permisos se pueden definir por vista, uasndo **class** o **decoradores**.

Todos los permisos heredan del **BasePErmissions** y tienen 2 métodos: **has_permissions y has_object_permission**. Y después Django tiene varios permisos configurados como: IsAuthenticated, IsAdminUser, IsAuthenticatedOrReadOnly (que sólo puede usar métodos seguros: GET, HEAD, OPTIONS), y más. También se pueden personalizar las configuraciones y permisos al sobreescribir **has_permissions y has_object_permissions**. Ej:
```python
class IsOwnerOrReadOnly(permissions.BasePermission):
  
    def has_object_permission(self, request, view, obj):
        # Read permissions are allowed to any request,
        # so we'll always allow GET, HEAD or OPTIONS requests.
        if request.method in permissions.SAFE_METHODS:
            return True

        # Instance must have an attribute named `owner`.
        return obj.owner == request.user
```
Recordar que en el **request** ya viene el **user**. 
En la docu oficial hay mas info de cómo customizar más los permisos.

- *[modificación: Noviembre 2020]*