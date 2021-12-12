# Docker

## Gestión de contenedores

### Lanzar un contenedor NGINX en modo segundo plano y que se ejecute en el puerto 80

```
sudo docker run -d -p 80:80 nginx
```

### Lanzar un contenedor NGINX en modo segundo plano y que se ejecute en el puerto 8080

```
sudo docker run -d -p 8080:80 nginx:latest
```

### Lanzar un contenedor con un nombre identificativo

```
sudo docker run -d -n NGINX -p 80:80 nginx:latest
```

### Lanzar un contenedor para ejecutar cosas en él

```
sudo docker run -ti centos:latest /bin/bash
```

### Mapear una unidad del SO en un contenedor

```
sudo docker run -ti -v /home/sincorchetes:/app centos:latest /bin/bash
```

### Listar los contenedores incluyendo los que no están en marcha

```
sudo docker ps -a
```

### Listar los contenedores que solo están en marcha

```
sudo docker ps
```

### Eliminar todos los contenedores incluyendo los que están en marcha, dieron error o no se han desplegado

```
sudo docker rm -f $(docker ps -a | awk '{print $1}' | tail -n +2)
```

### Eliminar todos los contenedores solo lo que están en marcha

```
sudo docker rm -f $(docker ps | awk '{print $1}' | tail -n +2)
```