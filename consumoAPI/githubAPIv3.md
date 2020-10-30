# Github API V3

En estas notas unicamente sintetizamos lo basico para empezar a consimir la API de GitHub y tener una idea de los temas previos que se necesitan, pero recomendamos visitar la pagina oficial de [GitHub](https://docs.github.com/es/free-pro-team@latest/rest) para tener toda la informacion con detalle.

## Ejemplos de la API de GitHub

### [Modelo](https://docs.github.com/es/free-pro-team@latest/rest/overview/resources-in-the-rest-api#modelo)

Todos los accesos de la API son a través de HTTPS y se accede desde `https://api.github.com` y todos los datos se enviaran y se reciben como JSON.
**Para mas informacion de este comando ir a esta [seccion](./curl.md/#Curl)**

```
$ curl -i https://api.github.com/users/octocat/orgs

> HTTP/1.1 200 OK
> Server: nginx
> Date: Fri, 12 Oct 2012 23:33:14 GMT
> Content-Type: application/json; charset=utf-8
> Connection: keep-alive
> Status: 200 OK
> ETag: "a00049ba79152d03380c34652f2cb612"
> X-GitHub-Media-Type: github.v3
> X-RateLimit-Limit: 5000
> X-RateLimit-Remaining: 4987
> X-RateLimit-Reset: 1350085394
> Content-Length: 5
> Cache-Control: max-age=0, private, must-revalidate
> X-Content-Type-Options: nosniff
```

### Representacion detallada / resumen

Cuando hacemos una solicitud general la respuesta de la API nos regresara información resumida, ya que regresarla todo de golpe significaría un trabajo extenuante en términos de computo cuando es poco probable que ocupemos cada uno de ellos.
Así que en lugar de eso nos mostrara un subconjunto de los atributos de este recurso.
Ya si hacemos una solicitud a un recurso en especifico este nos regresara toda la información que tenga acerca de este.


### [Autenticación](https://docs.github.com/es/free-pro-team@latest/rest/overview/resources-in-the-rest-api#autenticaci%C3%B3n-b%C3%A1sica)

Existen dos formas de autenticarce a través de la API V3 de Github.
La autenticacion basica que conciste de pasar el username y el password por medio de una solicitud y la autenticacion con Token de OAuth que es la forma mas recomendada por cuestiones de seguridad.
Si solicitamos entrar a una url en la que se necesita que estemos autenticados este nos regresara un error `404 Not Found` en lugar de un `403 Forbidden` para evitar filtramientos de repositorios a usuarios no autorizados.

*Puedes ver la documentacion de los comandos [aquí](./curl.md/#Curl)*

**Advertencia:** Github descontinuará la autenticacion basica a la API a partir del 5 de mayo del 2021

```
# Autenticacion basica

$ curl -u "username" https://api.github.com

```
```
# Autenticacion por OAuth

$ curl -H "Authorization: token OAUTH-TOKEN" https://api.github.com

```
#### Autenticacion fallida

Autenticarse con credenciales fallidas regresara el mensaje `401 Unauthorized:`

```
$ curl -i https://api.github.com -u foo:bar
> HTTP/1.1 401 Unauthorized

> {
>   "message": "Bad credentials",
>   "documentation_url": "https://developer.github.com/v3"
> }
```

Después de detectar varias solicitudes con credenciales inválidas dentro de un periodo de tiempo corto, la API rechazará temporalmente todos los intentos de autenticación para el usuario en cuestión (incluyendo aquellos con credenciales válidas) con el mensaje `403 Forbidden:`

```
$ curl -i https://api.github.com -u valid_username:valid_password
> HTTP/1.1 403 Forbidden

> {
>   "message": "Maximum number of login attempts exceeded. Please try again later.",
>   "documentation_url": "https://developer.github.com/v3"
> }
```

### [Parametros.](https://docs.github.com/es/free-pro-team@latest/rest/overview/resources-in-the-rest-api#par%C3%A1metros)

Muchos metodos de la API toman parametros opcionales, para las solicitudes de tipo `GET`, cualquier parametro que no sea parte de la ruta de la URL puede parsearse con el dato que necesitemos como un parametro de la secuencia de la consulta HTTP.

En este ejemplo, los valores 'vmg' and 'redcarpet' se proporcionan para los parámetros :owner y :repo en la ruta mientras que se pasa a :state en la secuencia de la consulta.
```
# URL con parametros opcionales
curl -i "https://api.github.com/repos/{owner}/{repo}/issues?state=closed"
```
```
# URL con los parametros parceados
curl -i "https://api.github.com/repos/vmg/redcarpet/issues?state=closed"
```

Para las solicitudes tipo `POST`, `PUT`, `PATCH` y `DELETE`, los parametros que no se incluyan en la URL deberan codificarse como `JSON` con un `Content-Type` de `'aplication/json'`

```
$ curl -i -u username -d '{"scopes":["public_repo"]}' https://api.github.com/authorizations
```

Para mas informacion acerca de las solicitudes HTTP visita la entrada [HTTP](./http.md/)

