# Github API V3

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