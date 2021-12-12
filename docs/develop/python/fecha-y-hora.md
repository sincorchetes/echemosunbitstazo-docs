# Fecha y hora

## Módulo time

Permite trabajar con la fecha y la hora, estos son algunos métodos.

```
import time
print(time.ctime())
```

Devolverá:

```
Mon Apr 13 21:58:46 2020
```

No es muy práctico si quieres hacer otras cosas, como asignar una fecha y hora a un archivo que quieras crear, por suerte, puedes preformatear con `.strftime()`.

```
 1import time
 2fecha_log = time.strftime("%d-%m-%Y_%H-%M-%S")
 3fecha_humano = time.strftime("%A %d %B %Y %H:%M:%S")
 4
 5# Imprimirá una fecha como esta:
 6# 13-04-2020_22-23-06
 7print(fecha_log)
 8
 9# Imprimirá una fecha como esta:
10# Monday 13 April 2020 22:23:06
11print(fecha_humano)
```

Puedes ver más información sobre los parámetros para formatear [aquí](https://docs.python.org/3/library/time.html#time.strftime)

Este es un ejemplo de como almacenar el resultado del comando dmesg del sistema operativo Linux, y que se almacene el resultado en un archivo con la fecha preformateada.

```
 1import subprocess
 2dmesg = subprocess.Popen(["dmesg"], shell=False,stdout=subprocess.PIPE)
 3
 4from time import strftime as ConvertirTiempoLog
 5fecha_log = ConvertirTiempoLog("%d-%m-%Y_%H-%M-%S")
 6archivo_log = "dmesg_log_%s.log" % (fecha_log)
 7
 8with open(archivo_log,'w') as dmesg_log:
 9  dmesg_log.write(dmesg.stdout.read().decode('utf-8'))
10  dmesg_log.close()
```

## Módulo calendar

Muestra un calendario como el comando `cal` de Linux.

```
 1import calendar
 2calendar.month(2020,1)
 3# Nos mostrará:
 4  January 2020
 5Mo Tu We Th Fr Sa Su
 6       1  2  3  4  5
 7 6  7  8  9 10 11 12
 813 14 15 16 17 18 19
 920 21 22 23 24 25 26
1027 28 29 30 31
```

Puedes hacer una combinación con el módulo `time` y `calendar`.

```
1import time,calendar
2anyo = int(time.strftime("%Y"))
3mes = int(time.strftime("%m"))
4
5#Imprimirá el calendario del año y me introducido.
6print(calendar.month(anyo,mes))
```

O también puedes hacer que devuelva un calendario con valores específicos:

```
1import calendar
2anyo = int(input("Introduzca el año a consultar: "))
3mes = int(input("Introduzca el mes: "))
4
5#Imprimirá el calendario del año y me introducido.
6print(calendar.month(anyo,mes))
```

Más información, en la documentación [oficial](https://docs.python.org/3/library/calendar.html)