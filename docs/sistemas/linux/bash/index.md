# Introducción

## ¿Qué es Bash?

Bash es un intérprete de comandos también conocido en inglés como una «*shell*» desarrollada el 8 de junio de 1989 por Brian Fox en el lenguaje C como alternativa y mejora de SH (*Bourne Shell*). Hoy en día es multiplataforma ya que puede correr tanto en Linux como en Mac OS X (de hecho es shell por defecto), en Windows mediante [Cygwin](https://www.cygwin.com/) o mediante la instalación oficial desde su apartado de añadir nuevas características de software.

Actualmente existen multitudes de I.C pero mencionaremos las más destacadas como:

- `csh`: C Shell creada por Bill Joy, 1978
- `tcsh`: TENEX C Shell desarrollada por Ken Greer, 1981
- `fish`: Shell interactiva liberada el 13 de febrero de 2005 por Axel Liljencrantz
- `zsh`: Z Shell elaborada por Paul Falstad en 1990
- `ksh`: KornShell creada por David Korn en 1983

Cada una de ellas contiene ciertos matices a la hora de desarrollar scripts que son un serie de ficheros que suelen contener comandos e intrucciones adicionales para que se puedan ejecutar sin tener que escribir grandes bloques de comandos, variables…

# Trabajando con Bash

## Directorios y archivos

En este apartado veremos como trabajar con los directorios dentro del sistema. Tenemos que tener en cuenta, de que la arquitectura estandar del sistema de ficheros en Linux (FHS) está organizada en modo de árbol. Esto quiere decir que todo cuelga de un directorio raíz llamado (/), del que cuelga el resto de ellos.

Nota

Comentaremos los directorios más básicos y relevantes para este artículo, ya que debe dedicársele un post solamente para explicar qué funciones realiza cada directorio del sistema.**

El directorio dónde por defecto se generan las carpetas para los nuevos usuarios del sistema se encuentra ubicado en `/home`. Por defecto, nuestra shell nos sitúa en el directorio principal de nuestro usuario, con lo que no tendremos que desplazarnos a niveles superiores dentro del sistema de archivos.

### Archivos ocultos

Los archivos ocultos se representan por llevar un `.` como prefijo al nombre del archivo o directorio y no aparecerán listados con ningún comando por defecto. No necesita ningún tipo de modificador adicional para generarlos o para leerlos.

### Rutas absolutas y relativas

Las rutas absolutas son aquellas que contienen la dirección completa dentro de la jerarquía del sistema de archivos. `/home/sincorchetes/Videos/Echemosunbitstazo/capitulo1.ogg`

Mientras que las rutas relativas, solo contienen una dirección breve que se muestra desde la propia carpeta. Imaginemos que estamos en el directorio `/home/sincorchetes/` y queremos llegar hasta el `capitulo1.ogg`. Para ello tendríamos que apuntar de la siguiente manera: `Echemosunbitstazo/capitulo1.ogg` ó bien `./Echemosunbitstazo/capitulo1.ogg`

### Escalado entre directorios

Nosotros podemos aprovecharnos de algunos «alias» que nos provee la shell para agilizar la gestión o administración de directorios haciendo uso de las rutas relativas. Estos son algunos trucos:

- `.`: Significa, el directorio actual. `ls .` devuelve una salida en la que mostrará todos los directorios y archivos en el directorio actual
- `..`: Sube un nivel superior, `ls ..` mostrará los directorios y archivos del directorio padre.

### Obtener la ruta del directorio actual

Si queremos saber en qué directorio nos encontramos actualmente, bastará con ejecutar el comando:

```
$ pwd
```

`pwd(1)` proviene del inglés «print name of current/working directory», imprimir el nombre del directorio actual.

### Creando un directorio

Con el siguiente comando generamos un directorio nuevo sin ningún tipo de contenido. Existe una sintaxis para crear directorios. No se puede empezar por caracteres especiales, aunque, dentro de los caracteres especiales se puede utilizar el espacio, pero se puede utilizar números, mayúsculas o minúsculas.

```
$ mkdir nombre_directorio
```

Nota

En caso de que queramos crear un subdirectorio sin existir primero el directorio padre, nos dará error si lo ejecutamos tal cual. Para ello, deberemos aplicar la opción `-p`.

### Desplazarnos entre directorios

Para poder desplazarnos entre directorios tenemos dos formas de hacerlo, mediante el comando UNIX por excelencia `cd(1)` o `pushd(1)` y `popd(1)`.

### Desplazándonos con cd

Simplemente deberemos ejecutar el comando y la ruta ya sea relativa o absoluta a la que queramos acceder como en los siguientes ejemplos:

- Situándonos en el directorio raíz del sistema: `cd /`
- Subiendo un nivel del directorio actual: `cd ..`
- Accediendo a `/usr/local/share`: `cd /usr/local/share`

### Desplazándonos mediante pushd y popd

Uno de estos comandos tienen la ventaja de almacenar en la sesión de `bash(1)` actual el directorio y además, nos ubica en él como es el caso de `pushd(1)`. Mientras que `popd(1)`, nos permite volver hacia atrás en caso de no querer seguir estando en él.

Moviéndonos al directorio raíz:

```
$ pushd .themes/
~/.themes ~
$ pwd
/home/sincorchetes/.themes
```

Volviendo hacia atrás:

```
$ popd
 popd
~
$ pwd
/home/sincorchetes
```

Estos comandos tienen algunas características especiales que podemos consultarlas en el manual de cada uno de ellos.

### Renombrando archivos y directorios

Para cambiar de nombre, solo será necesario ejecutar el comando mv(1) junto con el directorio que queramos cambiar y el directorio con nuevo nombre. Se pueden emplear rutas relativas, absolutas o una combinación de ambas:

- `mv dir dir_nuevo_nombre`
- `mv dir /home/sincorchetes/nuevo_nombre`
- `mv /home/sincorchetes/dir /home/sincorchetes/nuevo_nombre`

Nota

Hay que tener cuidado con utilizar `mv(1)` porque también sirve para mover directorios.**

### Moviendo archivos y directorios

Para desplazar directorios o archivos, tan solo tendremos que hacer uso de nuevo del comando `mv(1)`.

- `mv archivo.ogg /home/sincorchetes/Videos/Echemosunbitstazo`
- `mv archivo.ogg Videos/Echemosunbitstazo`
- `mv /home/sincorchetes/archivo.ogg Videos/Echemosunbitstazo`

También se puede aplicar un renombre más traslado:

- `mv archivo.ogg /home/sincorchetes/Videos/Echemosunbitstazo/nuevo_nombre.ogg`
- `mv archivo.ogg Videos/Echemosunbitstazo/nuevo_nombre.ogg`
- `mv /home/sincorchetes/archivo.ogg Videos/Echemosunbitstazo`
- `mv /home/sincorchetes/archivo.ogg /home/sincorchetes/Videos/Echemosunbitstazo`

### Copiando archivos y directorios

En el caso de copiar archivos, tenemos el comando `cp(1)`. También puede aplicarse el uso de rutas absolutas, relativas o un conjunto de las mismas. `cp archivo directorio_a_copiar`

Es importante destacar, que para copiar un directorio completo a pesar de que esté vacio. Hagamos uso del modificador `-r` o `-R` (_recursivo_)

También dispone de un modo interactivo utilizando el modificador `-i`

### Listar archivos y directorios

El comando por excelencia en estos casos es `ls(1)` Nos permite listar con multitudes de opciones si utilizamos los modificadores.

- Listar todos los archivos incluyendo los ocultos con la información que muestra `ls -l`: `ls -al`
- Mostar el nombre de todos los archivos incluyendo la representación del espacio como caracter escapado: `ls -b`
- Mostrar el nombre de todos los archivos en una sola columna: `ls -w 1`

### Tipos de archivo

En contra posición de sistemas como Windows, en Linux se puede tener un archivo sin ningún tipo de extensión. El sistema se encarga de averiguar que tipo de archivo es y abrirlo con la aplicación correspondiente.

Si queremos saber algún día si nos han enviado un ejecutable o un audio realmente, haremos uso del comando `file(1)`

### Crear un fichero vacío

Aunque la auténtica utilidad del comando `touch(1)` es modificar la fecha y hora de los archivos. También se puede utilizar para crear un fichero vacío y añadir texto posteriormente.

```
touch fichero_nuevo
```

### Mostrando información de un fichero

Si queremos leer un archivo de texto plano como la configuración de un servidor Apache, haremos uso del comando `cat(1)`.

```
cat /etc/profile
```

Salida truncada:

```
# /etc/profile

# System wide environment and startup programs, for login setup
# Functions and aliases go in /etc/bashrc

# It's NOT a good idea to change this file unless you know what you
# are doing. It's much better to create a custom.sh shell script in
# /etc/profile.d/ to make custom changes to your environment, as this
# will prevent the need for merging in future updates.

pathmunge () {
  case ":${PATH}:" in
    *:"$1":*)
    ;;
    *)
    if [ "$2" = "after" ] ; then
      PATH=$PATH:$1
    else
      PATH=$1:$PATH
    fi
    esac
}
```

## Trabajando con texto

### Mostrar o redireccionar texto

Bash nos permite mostrar una frase, un texto que queramos gracias al comando `echo(1)`.

```
echo "¡No nos perderemos los nuevos artículos de Echemosunbitstazo!"
```

También podemos redirigir el texto a un archivo nuevo

```
echo "¡No nos perderemos los nuevos artículos de Echemosunbitstazo!" > /home/sincorchetes/Documentos/archivo_nuevo
```

Añadir información a un archivo ya existente

```
echo "¡No te pierdas él próximo día otro capítulo más sobre Bash en echemosunbitstazo.es" >> /home/sincorchetes/Documento/existente
```

### Crear un archivo y añadir texto directamente

Podemos hacer uso del comando `cat(1)` para finalizar la edición, tendremos que finalizarla pulsando la combinación de teclas `CTRL+D` y para ello de la siguiente manera:

```
cat >fichero_de_ejemplo
Esto es un ejemplo.
```

## Copias de seguridad

El comando por excelencia para elaborar copias de seguridad en Linux es haciendo uso del comando `tar(1)`

### Elaborando copias de seguridad

### Elaborando una copia de un directorio

```
tar cfv copia_seguridad.tar dir1 dir2 archivo1 archivo2...
```

### Comprimir con bzip2

```
tar cfvj copia_Seguridad.tar.bz2 dir1 dir2 arch1 arch2...
```

### Utilizar compresión gzip

```
tar cfvz copia_seguridad.tar.gz dir1 dir2 arch1 arch2...
```

### Crear una copia de seguridad con formato xz

```
tar cfvJ copia_seguridad.tar.xz dir1 dir2 arch1 arch2...
```

### Descomprimiendo copias de seguridad

A la hora de descomprimir las copias de seguridad no tenemos que declarar el tipo de formato en el que está comprimido, con lo que ganamos más tiempo para dedicarlo a otras cosas.

### Descomprimir una copia de seguridad

```
tar xfv copia_seguridad.tar
```

## Comando grep

Este es uno de los comandos más esencial de Bash, nos permite mostrar coincidencias en archivos en base a la cadena de caracteres que nosotr@s le pasemos, en otras palabras, si queremos buscar una palabra en un archivo de texto, `grep(1)` es nuestro comando.

### Sintaxis y ejemplos

Acorde con las indicaciones que nos proporciona la todopoderosa biblia de los comandos, `man(1)` estos son 3 ejemplos que nos da `man 1 grep`.

```
grep [OPCIONES] PATRÓN [FICHERO...]
grep [OPCIONES] -e PATRÓN ... [FICHERO...]
grep [OPCIONES] -f FICHERO ... [FICHERO...]
```

Tanto las opciones, como los patrones y los ficheros se pueden repetir dentro de la línea de ejecución de nuestro comando.

Vamos con los ejemplos:

```
grep -o "Linux" /proc/version
```

Imprimirá la cadena «Linux» si la encuentra en el archivo, y la imprime tantas veces como la encuentre.

```
grep -q "Linux" /proc/version
```

No imprime nada, es una opción en la que se omite la salida, si encuentra una coincidencia con dicha palabra, devolverá en el estado de la shell un 0. `echo $?` = 0 si se encontró y = 1 en el caso contrario.

```
grep -H "sda" /proc/* 2>/dev/null
```

Muestra en cada línea en la que encuentre coincidencias, también el nombre del archivo y omite errores.

```
grep -A 2 "_this_module" /proc/kallsyms
```

Muestra las 2 líneas siguientes de haber encontrado la coincidencia en la o las líneas.

```
grep -B 2 "_this_module" /proc/kallsyms
```

La inversa de la anterior, en vez de mostrar las 2 líneas siguientes, muestra las dos líneas anteriores a la coincidencia.

```
grep -C 2 "_this_module" /proc/kallsyms
```

Si la A y la B hacía cada cosa por separado, con la C podemos mostrar tanto las líneas anteriores como las posteriores. En este caso muestra el resultado de las dos sentencias anteriores en una sola sentencia.

```
grep -rA 2 "gcc" /proc/ 2>/dev/null
```

Buscará de forma recursiva en todos los ficheros y directorios que se encuentren dentro del directorio especificado y cuándo obtenga una coincidencia, imprimirá las 2 líneas anteriores a la coincidencia incluyendo el nombre del archivo en el que se encuentre.

Nota

El uso del parámetro -r ya incluye el parámetro -H por defecto

```
grep -U "note" /bin/cp
```

Pretendemos encontrar una coincidencia dentro de un binario, y que en caso de encontrarla, ésta nos lo diga mediante un mensaje de salida.

```
grep -ob "root" /etc/passwd
```

Nos mostrará las líneas en dónde la coincidencia se haya repetido n veces dentro de un fichero especificado.

```
grep -obrA 2 "root" /etc 2>/dev/null
```

Permite efectuar lo mismo, pero se visualizarán las 2 líneas en cada coincidencia encontrada, número de línea, nombre de archivo dentro de un directorio y se omitirán los mensajes de error.

```
grep -FrB 2 '/usr' /proc 2>/dev/null
```

Permite utilizar caracteres especiales para la búsqueda de coincidencias. Este comando buscará de forma recursiva la cadena que contiene un carácter «prohibido» y mostrará las 2 líneas anteriores cada vez que encuentre una coincidencia. También omitirán los mensajes de error.

```
grep -ErC 2 '??linux' /proc 2>/dev/null
```

Al contrario que el anterior, aquí utilizaremos expresiones regulares como es el caso de ?? que sustituye a un caracter por signo de interrogación que no recordemos o no estemos seguro de cuál puede ser. Esta sentencia imprimirá las dos líneas siguientes a las coincidencias así mismo como las 2 anteriores, los mensajes de error se omitirán y se visualizará el nombre de los archivos que contengan dichas coincidencias

### fgrep y egrep

Pues ya los hemos dado en los dos ejemplos anteriores, aunque no lo creamos, `fgrep(1)` como `egrep(1)` son dos comandos que actúan como alias.

- `fgrep(1)` equivale a `grep -F`
- `egrep(1)` es igual a `grep -E`

## Alias

Los alias nos permiten reducir la longitud de una sentencia que queramos ejecutar en nuestro sistema y atajarla con una simple palabra. Por ejemplo, si queremos acceder a un directorio muy concurrido desde terminal.

```
cd ~/Documentos/Archivos/2018/05/10/10-11/Sector/1/ficheros_importantes/Codigo054/Area_51/
```

No nos imaginamos en absoluto tener que teclear toda esta ruta cada vez que queramos acceder al directorio Area_51. Pues podemos generar un alias, a nivel de sistema o a nivel de nuestro usuario.

A nivel de sistema, tenemos que añadirlo en `/etc/bashrc` si es que queremos que ese alias también lo tengan el resto de usuarios o si solo lo queremos para el nuestro, en ese caso, `~/.bashrc` es el que debemos tocar de la siguiente manera:

```
alias nombre_alias='cd ~/Documentos/Archivos/2018/05/10/10-11/Sector/1/ficheros_importantes/Codigo054/Area_51/'
```

Posteriormente aplicamos los cambios:

```
source /etc/bashrc
```

o si es a nivel usuario:

```
source ~/.bashrc
```

## Enlaces

Los enlaces vienen a ser lo que en Windows tenemos como «Accesos directos» pero a nivel de terminal, podemos especificar un directorio o un archivo que se encuentre en un directorio X pero teniendo un acceso más rápido en un directorio en el que trabajemos. También tenemos enlaces simbólicos que son accesos que si es borrado el archivo o directorio original solo queda el enlace y por lo tanto, no funciona y no es útil, o tenemos lo que denominamos enlaces duros, en los que se conserva una copia del fichero o directorio.

### Enlaces simbólicos

Para poderlos generar, simplemente tenemos que hacer uso del comando `ln(1)` con el parámetro `-s` de soft.

```
ln -s /directorio_a_enlazar /directorio_donde_quiero_ver_el_enlace
```

Por ejemplo:

```
ln -s /usr/src ~
```

Nos genera un enlace simbólico hacia el directorio `/usr/src` de nuestro `/home`.

¿Cómo averiguar si dispongo del enlace simbólico? Cuando hacemos un `ls(1)` para listar documentos y directorios, veremos en una de las líneas de salida un dato similar:

```
lrwxrwxrwx.  1 sincorchetes sincorchetes         9 May 20 17:37  src -> /usr/src/
```

- «l» al principio de esta entrada identifica un enlace simbólico.
- `src -> /usrc/src`: Nos dice hacia dónde apunta.

### Enlaces duros

Los enlaces duros permiten crear «una copia» de lo enlazado, de tal forma, que si se destruye el archivo o directorio original contínua funcionando.

```
ln /directorio_a_enlazar /directorio_donde_quiero_ver_el_enlace
```

De hecho, si hacemos un `ls(1)`, no veremos añadida una `l` en los permisos o en acceso tipo `src -> /usr/src`.

## Búsqueda de archivos

`find(1)` a diferencia de `locate(1)` es un comando que busca a tiempo real y tiene muchísimas funcionalidades añadidas como filtrar por nombre, tipo de ejecutable, fecha, hora…. e incluso, eliminar los ficheros que hemos querido encontrar, mientras que `locate(1)` trabaja junto con una base de datos generada por `updatedb(8)` reduciendo drásticamente la actualización puntera de la ubicación de los ficheros y directorios además de no tener la afinidad que posee `find(1)`.

[![https://asciinema.org/a/182400.png](https://asciinema.org/a/182400.png)](https://asciinema.org/a/182400)

### Comdando find

En este artículo vamos a guiarnos más por los ejemplos que por explicar la sintaxis o los parámetros de uno en uno.

Encontrar todos aquellos ficheros y directorios que se encuentren en el directorio `/etc`, y que aquellos directorios a los que no no podamos acceder a su contenido, no nos muestre el error de permisos.

```
find /etc 2>/dev/null
```

Encontrar todos aquellos archivos en `/var/` cuya extensión sea .log, y que por supuesto, no muestre aquellos directorios que requieran permisos para su acceso.

```
find /var -name "*.log" 2>/dev/null
```

Mostrar todos los directorios de nuestro `/home` sin contar los archivos

```
find ~ -type d
```

Encontrar archivos vacíos en nuestro `/home` y eliminarlos todos

```
find ~ -empty -type f -exec rm -rf {} \;
```

Encontrar ficheros con extensión .log y copiarlos en una carpeta dentro de nuestro home con permisos de superusuario

```
sudo find /var -name ".log" -exec cp {} /home/sincorchetes/LOGS \;
```

Buscando archivos cuya fecha de modificación sea de hace un minuto en nuestro `/home`

```
find ~ -cmin 1
```

Ficheros que han sido accedidos hace 10 minutos

```
find ~ -amin 10
```

Visualizar archivos que contengan .log de extensión, contengan permisos 644

```
sudo find /var -name "*.log" -perm 644
```

Ver archivos que pesen igual o redondeando den 2GB en nuestro directorio

```
find ~ -size 2G
```

Buscar directorios que contengan nuestro nombre de usuario, con permisos 777.

```
find / -user sincorchetes -type d -perm 777
```

Mostrar todos los archivos o directorios simbólicos que se encuentren en el directorio `/dev` y mostrarlo como si ejcutásemos un `ls(1)`

```
sudo find /dev -type l -ls
```

Listando aquellos archivos de nuestro `/home` cuya extensión contenga «`*`.avi» y sean iguales o superiores a 1G

```
find ~ -name "*.avi" -a -size 1G
```

Suprimiendo los .rpm que encontremos que lleguen a 10 megas

```
sudo find /var/cache/rpm -name "*.rpm" -a -size 10M -exec rm -rf {} \;
```

Podemos seguir ejemplos del manpages de `find(1)` o imaginarnos lo que se nos ocurra que podamos hacer en un futuro, estos son solo pequeños ejemplos de lo que podemos hacer con esta fantástica utilidad.

### Comdando locate

Bien, como hemos dicho anteriormente, este comando hace uso de una base de datos que por lo general suele ubicarse en `/var/lib/mlocate/mlocate.db`, y su fichero de configuración suele encontrarse en `/etc/updatedb.conf` todo depende de la distribución que utilicemos.

También podemos hacer un indexado que es registrar todos los archivos y directorios que queramos y se almacenen por un cierto orden en la base de datos de locate, sin tener que hacer uso de superusuario o creando un daemon en el sistema.

#### Regenerando las bases de datos

Podemos hacer que nos indexe todo lo que contenga el sistema y que lo puedan ver tod@s l@s usuari@s.

```
sudo updatedb
```

O bien, podemos generar una base de datos para nosotr@s.

```
mkdir .locateupdatedb -l 0 -U /DIR -o .locate/db_file
```

- `-l 0`: Permite entre otras cosas, crear el fichero de la base de datos utilizando nuestro usuario.
- `-U /DIR`: Directorio a idnexar
- `-o nombre_fichero`: El nombre que le pondremos a la db

Si queremos añadir más directorios, tendremos que ejecutar el comando modificando `/DIR`

#### Buscando archivos o directorios

Basta con ejecutar `locate nombre_archivo/nombre_dir` y el comando nos arrojará una salida completa con las coincidencias que encuentre en la db.

Sin embargo, si queremos ejecutar nuestro fichero, tendremos que especificárselo a `locate(1)`

```
locate nombre_directorio/nombre_archivo -d .locate/db_file
```

#### Visualizando estadísticas

Se pueden ver cuántos archivos y directorios tenemos actualmente registrados en cada db.

```
locate -S
```

ó

```
locate -Sd .locate/db_file
```

### Comando whereis

- Este comando nos viene de fábula cuando queremos encontrar algún binario, archivo fuente o incluso páginas de manual de `man(1)`, para hacerlo, este lleva una búsqueda en aquellos directorios que se encuentren declarados en la variable `$PATH` y `$MANPATH`. Estas variables las podemos encontrar en `/etc/profile` o en `~/.bash_profile`

  (en nuestro caso)

```
echo $PATH
```

Nuestra salida:

```
echo $PATH/usr/lib/qtchooser:/usr/local/bin:/usr/bin:/bin:/usr/local/sbin:/usr/sbin:/home/sincorchetes/.composer/vendor/bin:/home/sincorchetes/.local/bin:/home/sincorchetes/bin:/home/sincorchetes/.bin/scripts
```

Vamos a visualizar un par de ejemplos.

#### Buscando una página con la coincidencia

```
whereis -m cat
```

#### Encontrando la ubicación del binario

```
whereis -b cat
```

#### Buscando la fuente de un kernel de Fedora 28

```
whereis -s 4.16.8-300.fc28.
```

### Comando whatis

Este comando nos permite buscar en las páginas de `man(1)` y nos devuelve una descripción del mismo en una sola línea, en caso de que encuentre varios resultados, mostrará ambos o más y su categoría dentro de `man(1)`.

```
whatis cat
```

Salida:

```
cat (1p) - concatenate and print filescat (1) - concatenate files and print on the standard output
```

Podemos especificar un directorio diferente para que busque en otras páginas de `man(1)` pues que no tengamos instaladas en el directorio raíz o no se encuentren registradas en `~/.bash_profile`

```
whatis -M ~/.man/ cat
```

Entre otras cosas

### Comando apropos

Este comando es parecido al anterior, lo que utiliza directamente `mandb(1)`, también permite utilizar otra ruta de directorio para los manpages…etc

```
apropos whatis
```

Salida:

```
whatis (1) - display one-line manual page descriptions
```

## Redireccionamiento

Un redireccionamiento, como su propio nombre indica lo que hace es una redirección a un determinado sitio. En nuestro caso, utilizaremos los redireccionamientos para gestionar tanto las salidas, como entradas así como los niveles de error que de un comando o una aplicación para utilizarlos en nuestro beneficio.

Podemos decirle a un comando, que si tiene un error X, no lo muestre en pantalla y lo rediriga a un archivo de texto para que haga de log. También podemos añadir una frase, sentencias… a un archivo ya existente o en caso de que no exista que lo cree; comentar el número de palabras que tiene un texto… y un sin fin de cosas más.

### Operadores de redireccionamiento

Estos son los operadores que utilizaremos en la elaboración de scripts sobre todo, capítulo que introduciremos estos días con las siguientes entregas.

| Operador | Descripción                                                  |
| -------- | ------------------------------------------------------------ |
| `>`      | Redirecciona una salida hacia un archivo o comando. Si el archivo no existe, lo crea, y si existe, lo sobreescribe |
| `>>`     | Igual que el anterior, pero si el archivo existe no lo destruye, añade la salida después de la última línea |
| `<`      | Redirecciona una entrada hacia un comando para que este emita una salida (si lo hace), puede ser la salida de un comando hacia otro, un fichero… |
| `<<`     | Redirecciona el contenido de un fichero hasta que se encuentre la palabra especificada en la redirección para finalizarla |

### Canales

Nuestra terminal tiene una serie de canales por los que se toman la entrada, salida y errores.

+——-+ ——————————————————————-+————-+ | Canal | Descripción | Ubicación | +——-+ ——————————————————————-+————-+ | 0 | Es el canal por defecto de la entrada estándar | /dev/stdin | +——-+ ——————————————————————-+————-+ | 1 | Especifica la salida de un comando. Por ejemplo ls 2> file.txt | /dev/stdout | +——-+ ——————————————————————-+————-+ | 2 | Muestra la presencia de errores. Por ejemplo ls -lklk 3> error.txt | /dev/stderr | +——-+ ——————————————————————-+————-+

### Ejemplos

#### Almacenar la salida del comando ls -al en un fichero lista.txt

```
ls -al > lista.txt
```

Veremos como no se muestra nada en pantalla, pero se ha creado el archivo `lista.txt`

#### Mostrar el contenido de `lista.txt`

```
cat lista.txt
total 568
drwxrwxr-x.  2 sincorchetes sincorchetes  4096 May  2 01:43 .
drwx------. 55 sincorchetes sincorchetes  4096 May  2 17:10 ..
-rw-rw-r--.  1 sincorchetes sincorchetes 25277 May  1 12:55 20E2MC8SVX-9423.png
-rw-rw-r--.  1 sincorchetes sincorchetes 25277 May  1 12:55 36712GXM3C-865.png
-rw-rw-r--.  1 sincorchetes sincorchetes 25277 May  1 12:55 4SASA426RU.png
-rw-rw-r--.  1 sincorchetes sincorchetes 25277 May  2 01:43 5ODFPGZXOI-25637.png
-rw-rw-r--.  1 sincorchetes sincorchetes 25277 May  2 01:43 5PYBWDCZWK.png
-rw-rw-r--.  1 sincorchetes sincorchetes 25277 May  1 12:55 6A21WJKHWL.png
```

Nota

Recordemos que el operador `>` sobreescribe todo lo que haya, si queremos añadir información nueva al archivo debemos utilizar el operador `>>`

```
ls -al >> lista.txt
cat lista.txt
total 568
drwxrwxr-x.  2 sincorchetes sincorchetes  4096 May  2 01:43 .
drwx------. 55 sincorchetes sincorchetes  4096 May  2 17:10 ..
-rw-rw-r--.  1 sincorchetes sincorchetes 25277 May  1 12:55 20E2MC8SVX-9423.png
-rw-rw-r--.  1 sincorchetes sincorchetes 25277 May  1 12:55 36712GXM3C-865.png
-rw-rw-r--.  1 sincorchetes sincorchetes 25277 May  1 12:55 4SASA426RU.png
-rw-rw-r--.  1 sincorchetes sincorchetes 25277 May  2 01:43 5ODFPGZXOI-25637.png
-rw-rw-r--.  1 sincorchetes sincorchetes 25277 May  2 01:43 5PYBWDCZWK.png
-rw-rw-r--.  1 sincorchetes sincorchetes 25277 May  1 12:55 6A21WJKHWL.png
-rw-rw-r--.  1 sincorchetes sincorchetes 25277 May  2 01:43 6FG92BUEDM-12977.png
-rw-rw-r--.  1 sincorchetes sincorchetes 25277 May  2 01:43 A6XZFBO1TK-18309.png
-rw-rw-r--.  1 sincorchetes sincorchetes 25277 May  2 01:43 FBEBPAR2O9-16637.png
-rw-rw-r--.  1 sincorchetes sincorchetes 25277 May  2 01:43 FP9EZ05Y3E-16753.png
-rw-rw-r--.  1 sincorchetes sincorchetes 25277 May  1 12:55 FZRD6D42BI-875.png
```

#### Guardar todos los errores que surjan en la ejecución del programa

```
cat ks 2> error.txt
```

#### No se mostrará nada en pantalla, pero nos daremos cuenta el error que nos da `cat(1)` en el fichero que se ha creado llamado `error.txt`

```
cat error.txt
cat: jk: No such file or directory
```

#### Mostrar en pantalla tanto la salida estándar como los errores

```
ls -al 2>&1 info.txt
```

#### Guardar en un fichero tanto la salida como los errores

```
ls -al 2>&1 info.txt > file.txt
```

#### Calcular las líneas que tiene un fichero de texto

```
wc -l < file.text
```

#### Añadir información a un fichero e interrumpirlo utilizando una palabra clave declarada por el usuario

```
cat add << EOF
```

#### Crear un fichero de texto utilizando la canal de entrada y utilizando una palabra clave para finalizar la adicción

```
cat > create_text.txt << EOF
```

#### Adherir la salida estándar de múltiples textos y redireccionándolos a un archivo

```
cat lista.txt error.txt info.txt create_text.txt > salida_multiple
```

## Tuberías

Una tubería es una secuencia de uno o más comandos separados por operadores de control como `|` o `&`. Suelen utilizarse mucho junto con el comando `grep(1)`, `egrep(1)` y `fgrep(1)` para filtrar resultados, o el comando `cut(1)` para recortar la salida estándar, generalmente producida por comandos. Estos comandos que hemos mencionado les dedicaremos un post especial debido a la importancia de los mismos. Sobre todo cuando demos scripting más adelante.

### Este es el formato de una tubería común

```
comando [+parámetros] | ó & [comando1]
```

### Ejemplos

### Basándonos en esta estructura de directorios

```
.
├── fichero-0
├── fichero-1
├── fichero-10
├── fichero-11
├── fichero-12
├── fichero-13
├── fichero-14
├── fichero-15
├── fichero-16
├── fichero-17
├── fichero-18
├── fichero-19
├── fichero-2
├── fichero-3
├── fichero-4
├── fichero-5
├── fichero-6
├── fichero-7
├── fichero-8
└── fichero-9
```

### Mostrar un valor relacionado con `dmesg(1)`

```
dmesg |grep Bluetooth
[   23.265232] Bluetooth: Core ver 2.22
[   23.265247] Bluetooth: HCI device and connection manager initialized
[   23.265250] Bluetooth: HCI socket layer initialized
[   23.265251] Bluetooth: L2CAP socket layer initialized
[   23.265256] Bluetooth: SCO socket layer initialized
[   24.078796] Bluetooth: hci0: read Intel version: 370810225019140f18
[   24.078797] Bluetooth: hci0: Intel device is already patched. patch num: 18
[   35.047963] Bluetooth: BNEP (Ethernet Emulation) ver 1.3
[   35.047967] Bluetooth: BNEP filters: protocol multicast
[   35.047974] Bluetooth: BNEP socket layer initialized
[   85.419671] Bluetooth: RFCOMM TTY layer initialized
[   85.419675] Bluetooth: RFCOMM socket layer initialized
[   85.419722] Bluetooth: RFCOMM ver 1.11
[60146.891379] Bluetooth: hci0: read Intel version: 370810225019140f00
[60147.826024] Bluetooth: hci0: Intel Bluetooth firmware file: intel/ibt-hw-37.8.10-fw-22.50.19.14.f.bseq
[60148.097374] Bluetooth: hci0: Intel firmware patch completed and activated
[60151.506132] Bluetooth: hci0: command 0x0c56 tx timeout
```

### Mostrar un valor relacionado con la salida del comando `lspci(8)`

```
lspci |grep VGA00:02.0 VGA compatible controller: Intel Corporation Device 591b (rev 04)
```

## Fuentes

- Ediciones ENI - LPI I Tercera edición
- [IBM Knowledge Center](https://www.ibm.com/support/knowledgecenter)
- The Linux Documentation Project ~ [TLDP](https://www.tldp.org/LDP/abs/html)
- [IBM Knowledge Center](https://www.ibm.com/support/knowledgecenter)
- manpages: `find(1)`, `locate(1)`, `updatedb(1)`, `whereis(1)`, `whatis(1)`, `apropos(1)`, `ln(1)`, `ls(1)`, `help if`