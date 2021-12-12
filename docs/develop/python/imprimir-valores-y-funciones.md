# Imprimir valores y funciones

## Sustitución de tipos de datos en sentencias print()

Cuando queremos incluir un valor que proviene de variables, listas, sets, tuplas… se pueden hacer de múltiples formas. Por ejemplo:

```
variable = "Susana"
print("Hola me llamo:", variable)
Hola me llamo Susana.
```

Podemos hacerlo de esta forma:

```
variable = "Susana"
print("Hola me llamo: %s" % variable)
Hola me llamo Susana.
```

Tenemos que tener en cuenta que de esta manera, hay que definir si el dato que vamos a sustituir es `str` = `%s%`, `int` = `%i`, `float` = `%f`.

Nota

Los valores de tipo `complex` = `%c` no tienen sustitución directa en esta forma, por lo que hay que utilizar otro método como en el anterior.

O de esta otra:

```
variable = Susana
print(f'Hola me llamo {variable}')
```

También tenemos esta otra:

```
variable = "Susana"
print("Hola me llamo {}".format(variable))
```

En fin, hay muchas formas de hacer sustituciones en los `str` y en otros tipos de datos que puedes consultar en la [documentación oficial](https://docs.python.org/3/tutorial/inputoutput.html)

## Iteradores

Un iterador es una especie de puntero que permite devolver valores que le especifiquemos.

```
 lista= ["Hola","esto","es","un","ejemplo","de","iterador"]
 
 # Inicializamos el iterador
 mi_iterador = iter(lista)
 
 # Se puede imprimir el valor de esta manera, que devuelve la palabra Hola
 print(next(mi_iterador))
 
 # Pasamos al siguiente iterador que contiene la palabra "esto", pero no la imprimimos.
next(mi_iterador)

# Imprimimos la palabra "es"
print(next(mi_iterador))

# Imprimir todos los elementos del iterador:
for item in mi_iterador:
  print(item)
```

## Funciones

Conjunto de código organizado y que contienen una serie de instrucciones que pueden reutilizarse. Por ejemplo, `dormir` es una función que tenemos, hay múltiples variables como el lugar, la intensidad de la luz, si estamos cómodos… pero que al final el resultado es descansar. Lo mismo sucede con las funciones.

Declaración de ejemplo de una función:

```
def my_funcion():
  # Bloque de código
```

### return

```
return` permite devolver un valor de la función y darla por terminada más que utilizar un `print()
def func(a):
  return a

valor=func(12)
print(valor)
```

### yield

En contra posición de `return`, `yield` permite seguir aplicando el código que venga más adelante de la función creando una especie de co-rutina o gestión de resultados o ejecución por turnos, como si fuera un corredor de atletismo que le pasa el testigo a otro y su marca de tiempo es el valor de retorno. Hacemos uso de los iteradores para extraer los datos.

```
 def func(a):
   print("Devolvemos el primer resultado: %i" % (a))
   yield a
   c = a - 2
   print("Devolvemos el segundo valor: %i" % (c))
   yield c
 
 abc = func(20)
 
mi_iter = iter(abc)

for item in mi_iter:
    print(item)
```

## Tipos de funciones en Python

En Python, tenemos 2 tipos de funciones, una que creamos nosotros y otras que vienen integradas. Las que nosotros creamos las definimos en nuestra aplicación, script… mientras que las integradas, vienen con la instalación de Python que ya fueron elaboradas y que puedes utilizar como: `len()`, `max()`, `min(), :code:`type()`, `range()`…

Veamos un ejemplo:

```
>>> def hola_mundo():
>>>   print("Hola Mundo")
>>> hola_mundo()
Hola Mundo
```

Podemos pasar todo tipo de valores, por ejemplo, pasaremos una lista como valor y un número entero:

```
>>> lugares = [ "Toronto", "Tokio", "Nueva Zelanda" ]

>>> def mostrar_lugares(valores):
>>>   for lugar in valores:
>>>     print(lugar)
>>> mostrar_lugares(lugares)
Toronto
Tokio
Nueva Zelanda
```

## Asignar una función a una variable

Podemos asignar una función a una variable y llamarla como función desde la propia variable:

```
def mensaje(msg):
    print(msg)

segundo=mensaje

# Imprime "Mundo"
segundo("Mundo")
```

## Asignar valores por defecto a los argumentos

Si no le decimos o especificamos un valor cuando llamamos a la función, podemos hacer que tome parámetros por defecto.

```
def test(variable="Valor que queremos")
  print(variable)

test()
```

Esto devolverá «Valor que queremos», si especificamos un valor tal que así:

```
test("Hola mundo")
```

Devolverá `Hola mundo`

## Closures

Los closures es un objeto especial que permite obtener información de otras funciones hijas que forman parte de una función padre, permiten dar más seguridad al código ya que todo lo que tenga que ejecutarse se hará dentro de ese ámbito o *scope*.

Ejemplo de closure:

```
def func(x):
    def func_a():
        print(x)
    return func_a()
```

## Generadores

Son funciones que crean iteradores, estas funciones realmente son objetos en Python. Si hacemos un print sobre la función, veremos `<generator object mensaje at 0x7f31a4957250>`, es muy importante saberlo.

No solo podemos trabajar con `return`, también con `yield`.

```
 def mensaje(msg):
     def lector():
         print(msg, "%s" % ("leido por un lector."))
     def escritor():
         print(msg, "%s" % ("escrito por un escritor."))
 
     yield lector()
     yield escritor()
 
ejemplo = mensaje("Alguien escribió este mensaje y ha sido")

for item in ejemplo:
    if item is None:
        pass
    else:
        print(item)
```

## Función Lambda

Esta función no tiene nombre también se le conoce como función anónima, sin embargo, no puede contener más de una expresión:

```
>>> x = lambda a : a + 10
>>> resultado = x(5)
>>> print(resultado)
15
```

Si lo pasamos a función esto sería así:

```
>>> def sumar(a,b):
>>>   return a + b
>>> sumar(5,10)
15
```