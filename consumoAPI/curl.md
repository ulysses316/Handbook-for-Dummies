# CURL

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


