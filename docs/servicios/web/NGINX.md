# NGINX

## Introducción

Es un servidor HTTP que puede actuar como proxy reverso de tipo HTTP, correo electrónico o TCP/UDP. Fue desarrollado por Igor Sysoev, distribuido bajo licencia de tipo [BSD de 2 cláusulas](http://nginx.org/LICENSE), tiene soporte comercial [Nginx, Inc.](https://www.nginx.com/) y ha sido ejecutado desde hace tiempo en sitios web rusos como [Yandex](http://www.yandex.ru/), [Mail.Ru](http://mail.ru/), [VK](http://vk.com/), and [Rambler](http://www.rambler.ru/), y que también utilizan servicios como [Dropbox](https://blogs.dropbox.com/tech/2017/09/optimizing-web-servers-for-high-throughput-and-low-latency/), [Netflix](https://openconnect.netflix.com/en/software/), [Wordpress.com](https://www.nginx.com/case-studies/nginx-wordpress-com/), [FastMail.FM](http://blog.fastmail.fm/2007/01/04/webimappop-frontend-proxies-changed-to-nginx/).

## Instalación

> Nota: Esta documentación está elaborada para Rocky Linux, deberás buscar tus adaptaciones para la distribución que utilices.

```bash
sudo dnf install -y nginx
```

## Gestión del servicio

Iniciando el servicio

```bash
sudo systemctl start nginx.service
```

Parando el servicio

```bash
sudo systemctl stop nginx.service
```

Obteniendo el estado del servicio

```bash
sudo systemctl status nginx.service
```

Recargando el servicio sin pararlo

```bash
sudo systemctl reload nginx.service
```

Habilitando el servicio en el arranque

```bash
sudo systemctl enable nginx.service
```

Deshabilitando el servicio en el arranque

```bash
sudo systemctl disable nginx.service
```

Comprobar si el servicio está habilitado en el arranque

```bash
sudo systemctl is-enabled nginx.service
```

### Estructura del fichero de configuración

Está basado en módulos que se controlan por directivas definidas en archivos de configuración específicos. La sintaxis parte de un nombre y parámetros separados por espacios y que terminan en (;). Sin embargo, tenemos directivas que se encuentran dentro de una serie de bloques que empiezan y terminan con llaves ({ }) como podemos ver en el siguiente ejemplo:

```
server {
  listen 80;
}
```

Por supuesto, dentro de la documentación de cada módulo, podemos ver que se pueden anidar bloques de bloques como es el caso de  [events](http://nginx.org/en/docs/ngx_core_module.html#events), [http](http://nginx.org/en/docs/http/ngx_http_core_module.html#http), [server](http://nginx.org/en/docs/http/ngx_http_core_module.html#server), y [location](http://nginx.org/en/docs/http/ngx_http_core_module.html#location) este tipo de configuración recibe el nombre de contexto.

```bash
http {
  server {
    listen 80;
  }
}
```

La configuración se puede almacenar en el fichero troncal ubicado en `/etc/nginx/nginx.conf`, sin embargo, se pueden almacenar en `/etc/nginx/conf.d/` cuya extensión del archivo debe ser `.conf`.

## Conceptos

> NOTA: Recomiendo la búsqueda de qué es URI o URL en el glosario facilitado por la Mozilla Foundation que puedes encontrar [aquí](https://developer.mozilla.org/en-US/docs/Glossary)

### `Server block`

Los `Server Blocks`, son bloques de directivas pertenecientes al módulo [`server`](http://nginx.org/en/docs/http/ngx_http_core_module.html#server) y que se utilizan para servir o redirigir (_reverse proxy_) según el URI que configuremos.

```
server {
}
```

Éstos deben diferenciarse por puerto y por nombre del servidor, ya que nosotros podemos dar servicio a otros dominios con un mismo servidor. NGINX decidirá qué servidor procesará la petición, y posteriormente comprobará la URI especificada en la URL. Esta URI puede configurarse añadiendo un bloque con `location`.

```
server {
  listen 80;
  server_name example.com;
  location URI {
  }
}
```











