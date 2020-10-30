# CURL

En estas notas unicamente sintetizamos los comandos mas usados de CURL para empezar a hacer consultas a servidores, pero recomendamos altamente leer el manual de CURL con el comando.
```
$ man curl
```
Ademas de checar otras fuentes, para tener un mejor panorama del tema.

## ¿Que es?

**curl** es una herramienta para transmitir informacion desde/hacia un servidor, utilizando alguno de los protocolos que este soporta.

**curl** ofrece una serie de opciones bastante utiles como, soporto proxy, autenticacion de usuarios, carga FTP, publicacion HTTP, conexiones SSL, cookies, resumen transferencia de archivos entre otras cosas.

## Ejemplos de la API de GitHub

### [Modelo](https://docs.github.com/es/free-pro-team@latest/rest/overview/resources-in-the-rest-api#modelo)

Todos los accesos de la API son a través de HTTPS y se accede desde `https://api.github.com` y todos los datos se enviaran y se reciben como JSON.

### Comandos y banderas usados en la documentacion.

- **curl [options] [URL...]**

    - **-i, --include**

    > Incluye los headers de la respuesta HTTP en la salida. Los headers pueden incluir informacion como nombre del servidor, cookies, fecha del documento, version HTTP entre otras cosas.


    - **-u, --user**
    
    > Especifica el nombre de usuario y la contraseña a usar para la autenticacion en el servidor(No se recomienda poner la contraseña directamente en el comando por motivos de seguridad)
    la mejor manera es poner unicamente el username y directamente curl nos pedira despues la contraseña
    
    > Hay especificaciones para unos tipos de servidores que se recomienda checar en la documentacion.
    `$ man curl`

    - **-H, --header**
    > Este es un encabezado adicional para incuir en la solicitud http que se enviara al servidor. Se pueden agregar cualquier cantidad de encabezados adicionales. **NOTE** En dado caso que uno de sus encabezados que declare tengan el mismo nombre que uno de los encabezados que utiliza curl internamente se usara el suyo en lugar del origina. Se recomienda que no se haga esto al menos que sepa completamente lo que esta haciendo.

    ```
    # Estructura de un header

    $ curl -H "X-First-name: Joe" http://example.com/

    ```

    En el ejemplo anterior vemos una declaracion de header, donde le mandamos un nuestro encabezado personalizado un parametro llamado 'X-First-name' que tiene el valor de Joe.
    En el caso de la API de github para hacer una autenticacion con OAuth lo hariamos de la siguiente manera.

    ```
    # OAuth Github API V3

    $ curl -H "Authorization: token OAUTH-TOKEN" https://api.github.com
    ```

    - **-d, --data**
    > (HTTP) Envia los datos especificados en una solicitud POST al servidor HTTP, del mismo modo que el navegador lo hace cuando un usuario rellena un formulario en el HTML y presiona el boton "enviar". Eso hara que curl pase los datos usando el `content-type application/x-www-form-urlencoded`