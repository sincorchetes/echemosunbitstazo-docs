## Módulos

¿Qué son los módulos? Los módulos son fragmentos de código que contienen librerías… que elaboran otros usuarios o que ya vienen integradas con Python. Hay muchos módulos que vienen ya pre-instalados en el sistema como pueden ser `os` que permite interactuar con el sistema operativo; `subprocess` que permite ejecutar comandos de shell; `json` con el que podremos trabajar con archivos o salidas JSON…

### ¿Cómo cargar este código?

El código de los módulos puede cargarse utilizando la palabra `import`, como en el siguiente ejemplo:

```
>>> import json
```

También podemos cargar parte del código de los módulos como por ejemplo `random` es un módulo que contiene métodos y propiedades. Podemos cargar solo uno de los métodos que tienes como es `.random()` y asignarle un alias para trabajar con él como en le siguiente ejemplo:

```
>>> from random import random as GenerarAleatorio
>>> GenerarAleatorio()
0.9037083824066462
```

### ¿Qué pasa si no me sé las propiedades o métodos de un módulo?

No pasa nada, puedes revisar siempre la documentación de Python pulsando [aquí](https://docs.python.org/3/)