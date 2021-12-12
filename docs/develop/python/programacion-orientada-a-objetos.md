# Programación orientada a objetos

Python es un lenguaje como ya mencionamos anteriormente orientado a objetos. Los objetos contienen una serie de métodos y propiedades que lo definen. Si pensamos en un humano, tenemos como propiedades el color de ojos, color de piel, altura… y los métodos serían las acciones como el baile, leer, saltar, correr…

Esta metodología de programación nos permite reusar el código las veces que queramos sin tener que estar escribiendo múltiples líneas con funciones específicas para determinadas partes de nuestro código si lo hicieramos en una programacioń estructurada o procedural.

## Principios básicos

En Python tenemos los siguientes principios:

- **Clase**: Tipo de dato que contiene un esquema de métodos y propiedades que se usarán para construir un objeto.
- **Objeto**: Una clase que se ha inicializado, es decir, existe y tiene nombres y apellidos propios en su ejecucioń.
- **Herencia**: Propiedades o métodos que ha recibido una clase hija por parte de una clase padre, esto no quiere decir que vaya a heredar todos los métodos y propiedades, solo aquellos que se le permitan.
- **Encapsulación**: La habilidad de enseñar aquello que solo se pueda mostrar y esconder lo que no nos interesa visibilizar.
- **Polimorfismo**: La capacidad que tiene un objeto para cambiar su rol al mismo tiempo, puede actuar de un rol y en otro rol al mismo tiempo.

### ¿Qué es una clase?

Una clase es la plantilla que tendrá el objeto que queremos crear, contiene una serie de méotodos y propiedades que los utilizaremos una vez generemos el objeto. Por supuesto, una clase es un tipo de dato dentro de Python.

### ¿Cómo declaramos una clase?

Para generar una clase seguiremos esta sintaxis:

```
class NombreClase:
  # Bloque de código
```

### ¿Cómo podemos añadirle propiedades y métodos a una clase?

De la siguiente forma:

```
class Coche:
  propiedad = valor

  def método(self):
    # Bloque de código
```

Un ejemplo podría ser:

```
class Coche:
  marca = "Toyota"
  modelo = "Corolla"

  def publicidad(self):
    print("De 0 a 100 en 10 segundos")
```

Tenemos la clase Coche, con unas propiedades definidas que son la marca y el modelo, además, tenemos un método llamado publicidad que muestra un mensaje. En el siguiente apartado, veremos como trabajar con esta clase pero desde la vista de un objeto.

### ¿Qué es un objeto?

Un objeto es la materialización de una clase, es decir, cuando lo generamos a partir de unas instrucciones ya empieza a existir en nuestro programa que estemos desarrollando. Por ejemplo, tenemos la clase Casa, evidentemente, las casas que declaremos tiene propiedades y métodos diferentes, por ejemplo, tiene una dirección, un número, una elevación, una función, un espacio diferente. Si creamos 5 casas, hemos creado 5 objetos partiendo de una sola clase que es la clase Casa.

En resumen:

- Es la unidad básica de POO
- Representa una instancia particular partiendo de una clase
- Puede haber más instancias partiendo de una misma clase
- Cada objeto puede contener y mantener su información

#### ¿Cómo declaramos un objeto?

La sintaxis es:

```
NombreObjeto = NombreClase()
```

En este ejemplo creamos 3 objetos diferentes partiendo de la clase anterior.

```
NombreObjeto = NombreClase()
NombreObjeto2 = NombreClase()
NombreObjeto3 = NombreClase()
```

#### Para acceder a sus propiedades

```
NombreObjeto.propiedad1
```

#### Para acceder a sus métodos

```
NombreObjeto.método1()
```

Utilizando el ejemplo que hemos creado antes:

```
class Coche:
  marca = "Toyota"
  modelo = "Corolla"
  publicidad = "De 0 a 100 en 10 segundos"

  def eslogan(self):
    print("Este es un método",self.publicidad)

Sara = Coche()
Ionela = Coche()
```

Tenemos a dos personas que utilizan el mismo coche Ionela y Sara y lo vemos:

```
print(Ionela.marca,Ionela.modelo)
Toyota Corolla
Ionela.eslogan()
De 0 a 100 en 10 segundos

print(Sara.marca,Sara.modelo)
Toyota Corolla
Sara.eslogan()
De 0 a 100 en 10 segundos
```

¿Qué pasa si Sara quiere cambiar de coche?

```
Sara.marca = "Citröen"
Sara.modelo = "Xsara"
Sara.publicidad = "El confort no es discutible."
print(Sara.marca,Sara.modelo)
Citröen Xsara
Sara.eslogan()
El confort no es discutible.
```

¿Pero Ionela ha cambiado de coche?

```
print(Ionela.marca,Ionela.modelo)
Toyota Corolla
Ionela.eslogan()
De 0 a 100 en 10 segundos
```

¡Ya lo tenemos! Podemos instanciar objetos diferentes partiendo de una misma clase y cambiar sus propiedades sin afectar al resto de objetos. ¿A qué es sencillo? Pero, ¿Qué pasa si queremos cualquier persona pueda tener un coche diferente desde el principio?

Pues a pesar de que se puede hacer creando un método que le asigne el valor a las propiedades, lo más correcto es utilizando el método `__init__`. Este método `constructor` (que permite inicializar un objeto) asigna valores a las propiedades del objeto cuando se construye, por ejemplo.

```
class NombreClase:
  def __init__(self, valor_propiedad1, valor_propiedad2):
    self.propiedad1 = valor_propiedad1
    self.propiedad2 = valor_propiedad2

  def metodo1(self):
    # Bloque de código
```

Para crear el objeto:

```
Variable=NombreClase("Valor de ejemplo n1","Valor de ejemplo n2")
```

Si parece dificultoso de entender, no pasa nada, este es otro ejemplo con comentarios (*¡Será por ejemplos!*):

```
# Definimos la clase Coche
class Coche:

  # Definimos el constructor que sustituirá los
  # valores de las propiedades cuando las definamos al inicializar el objeto.

  def __init__(self,marca,modelo, velocidad):
    self.marca = marca
    self.modelo = modelo
    self.velocidad = velocidad

  # Cuando se llama a este método la velocidad se incrementa +1.
  def acelerar(self):
    self.velocidad += 1
    print(self.velocidad)

  # Cuando se llama a este método la velocidad disminuye en -1.
  def frenar(self):
    self.velocidad -= 1
    print(self.velocidad)

  # Creamos los objetos:

  Chami = Coche("Nissan", "Almera", 0)
  Jose = Coche("Toyota","Corolla AE92 GTi Twin Cam", 0)

  # Imprimimos los valores que tienen las propiedades de cada objeto:

  print("El coche de Chami es un:",Chami.marca,Chami.modelo,"y ahora va a",Chami.velocidad,"km/h.")
  print("El coche de Jose es un:",Jose.marca,Jose.modelo,"y ahora va a",Jose.velocidad,"km/h.")

  # Aumentamos la velocidad a uno de los objetos:
  Chami.acelerar()

  # Si queremos aumentar más veces la velocidad, podemos usar un bucle
  for x in range(0, 100):
    Chami.acelerar()

  # Imprimimos la velocidad actual
  print("Chami va a una velocidad de %i" % Chami.velocidad)
```

Este ejemplo si lo ejecutamos dará como resultado:

```
El coche de Chami es un: Nissan Almaera y ahora va a 0 km/h.
El coche de Jose es un: Toyota Corolla AE92 GTi Twin Cam y ahora va a 0 km/h.
```

## Herencia

Una de las propiedades que mencionamos que podían tener los objetos es la herencia, por lo que una clase hija puede contener propiedades y métodos de una clase padre. Veamos un ejemplo:

```
# Definimos la clase padre:
class ClasePadre:
# Decimos que se ejecute el código sin hacer nada.
  pass

# Y aquí la clase hija:
class ClaseHija(ClasePadre):
  pass

# Creamos el objeto
Objeto = ClaseHija()
```

Este es un ejemplo:

```
# Definimos la clase Familia
class Familia():

  # Con sus propiedades que se rellenarán cuando se inicialice el objeto.
  def __init__(self, miembros, apellidos):
    self.miembros = miembros
    self.apellidos = apellidos

    # Cuando se cree la clase, mostrará el apellido que ha recibido.
    print("Apellidos: %s" % (self.apellidos))

# Creamos la clase Hijo que hereda de Familia
class Hijo(Familia):

  # Se rellenarán propiedades para este objeto.
  def __init__(self, nombre, apellidos):

  # Si queremos heredar propiedades y métodos, tendremos que hacer uso de la función super()
  # super() lo explicaremos más adelante.
  # Aquí llamamos la propiedad específica de Familia, Familia.apellidos y la inicializamos
    super().__init__(self,apellidos)

  # Definimos aquí los valores que tendrán estas propiedades
    self.nombre = nombre
    self.apellidos = apellidos

# Añadimos un método para el Hijo
  def mostrar_info(self):

    # Decimos que imprima self.nombre y self.apellidos.
    print("Soy %s y soy de la familia %s" % (self.nombre,self.apellidos))

# Creamos el objeto
Pugsley = Hijo("Pugsley","Adams")

# Llamamos al método mostrar_info()
Pugsley.mostrar_info()
```

Seguro que te preguntas sobre `super().__init__(...)`, esta función como comentamos permite heredar propiedades y métodos de otra clase. Vendría a ser lo mismo que:

```
class A:
  def __init__(self, ejemplo):
    self.ejemplo = ejemplo

class B(A):
  def __init__(self, x, y, z):

    # Este procedimiento es más complicado y más tedioso de hacer.
    self.guardar_info = A(x)

obj = B(2,3,4)
print(obj.guardar_info.ejemplo)
```

### Sobreescribiendo métodos en clases hijas

Se puede hacer evidentemente, si en la clase A tenemos un método llamado `saludar()`, y la clase B que hereda de la clase A, le podemos definir el contenido del mensaje que devolverá el método `saludar()`.

```
 class A:
   def saludar(self):
     print("Hola mundo")
 
 class B(A):
   def saludar(self):
     print("Hello everybody")
 
 obj = B
 obj.saludar()
```

Y devolverá `Hello everybody`.

### Tipos de herencia

Bien, habiendo visto un ejemplo de herencia, también os cuento, que hay distintos ejemplos de herencia:

- Simple
- Múltiple
- Multi nivel
- Jerárquica
- Híbrida

#### Simple

Es el tipo de herencia que hemos visto hasta ahora.

```
class A:
  pass
class B(A):
  pass
```

#### Múltiple

Es una clase que hereda desde otras clases, por lo que tendrá propiedades y métodos de ambas clases (A y B).

```
 class A:
   pass
 class B:
   pass
 class C(A,B):
   pass
 
 # Establecemos una comparación para ver si realmente son subclases o no.
 # Devolverá True o False dependiendo de si es correcto o no.
 issubclass(C,A) and issubclass(C,B)
```

#### Multinivel

Esto se refiere, a que tenemos una clase abuelo, de la cuál hereda una clase padre, del cuál hereda una clase hijo.

```
class A:
  pass
class B(A):
  pass
class C(B):
  pass
```

Como vemos, la clase C hereda de la clase B, la clase B de la clase A, y A es la clase principial de primer nivel. Por lo tanto, la clase C herederá propiedades y métodos de todas sus clases superiores a menos que se establezca qué propiedades o métodos se podrán heredar, esto forma parte del encapsulamiento que veremos más tarde.

#### Jerárquica

Tenemos múltiples clases que heredan de una sola clase, es decir.

```
class A:
  pass
class B(A):
  pass
class C(A):
  pass
class D(A):
  pass
```

Un ejemplo puede ser, clase Jefe/Jefa de una empresa que tiene el rol más alto de una organización y que por debajo de ellos hay otros roles acordes a la labor de la empresa que tienen menos privilegios, otras funciones…etc

#### Híbrido

Es la combinación de una o múltiples clases con una o múltiples clases por ejemplo: Imaginamos que tenemos 5 clases (A,B,C,D,E).

- Clase A es una clase padre.
- Clase B,C,D heredan de la clase A
- Clase E, hereda de la clase B y D.
- Clase E es la clase padre de B y D.

Aquí podemos identificar varios tipos de herencia:

- A, B, C, D, C = **Herencia híbrida**
- B, C, D que heredan de A = **Herencia jerárquica**
- E que hereda de B y D = **Herencia múltiple**
- C hereda de A = **Herencia simple**

Un ejemplo de sintaxis:

```
class A:
  pass
class B(A):
  pass
class C(A):
  pass
class D(A):
  pass
class E(B,D)
```

Si añadimos una variable en la clase A, creamos un objeto que referencie a E:

```
class A:
  hello_world = "Hola Mundo"
class B(A):
  pass
class C(A):
  pass
class D(A):
  pass
class E(B,D):
  pass
obj = E()
  print(obj.hello_world)
```

`obj` habrá impreso `"Hola Mundo"`.

### Función super()

Se utiliza para llamar a métodos de una clase padre, hemos visto en un ejemplo anterior como llamábamos a `super().__init__(self, nombre, apellidos)` en el ejemplo de la Familia Adams. Aquí estábamos llamando al método inicializador de la clase `Familia`. Pero podemos llamar a otros métodos también. `super().método()`.

```
class Vehiculo:
  def arrancar(self):
    print("Arrancamos el coche")
  def parar(self):
    print("Paramos el coche")

class Conductor(Vehiculo):
  def soplar(self):
    print("Soplando, soplando y soplando...")

  def control_policia(self):
    super().parar()
    print("Persona - Hola agente, buenos días")
    print("Policía - Hola, vamos hacerle una prueba de alcoholemia, por favor, sople en la boquilla")
    print("Persona - Vale")
    self.soplar()
    print("Policía - Genial, puede usted proseguir")
    super().arrancar()

Antonio = Conductor()
Antonio.control_policia()
```

Como vemos, no hace falta que llamemos a `__init__` porque __no estamos inicializando ningún valor en ninguna propiedad `__` y como se ejecutan los métodos `parar()` y `arrancar()` que forman parte de la clase `Vehiculo`.

## Encapsulamiento

Encapsular permite abstraer cierta información al mundo y mostrar solo aquella que interese. Por ejemplo, cuando enviamos un paquete por correos, el personal de correos no puede ver el contenido del paquete, pero si que puede ver el destinatario y el remitente, pudiendo identificar a las dos personas implicadas y saber sus direcciones de correo postal.

### ¿Cómo encapsular?

Para encapsular, básicamente tendremos que añadirle dos guiones bajos `"_ __ _ "` delante de la propiedad que queremos ocultar.

```
class A:
  self._propiedad = valor
```

Veamos un ejemplo:

```
class Persona:
  def __init__(self):
    self.nombre  = "Susana"
    self.__apellidos = "Bramura"
    self._tlfno = "777 777 777"

Carlos = Persona()

print(Carlos.apellidos)
```

Veremos un error parecido a este:

```
Traceback (most recent call last):
  File "main.py", line 9, in <module>
    print(Carlos.apellidos)
AttributeError: 'Persona' object has no attribute 'apellidos'
```

Y nos preguntaremos… Pero, si llamamos a `Carlos.apellidos` y nosotros hemos puesto: `Carlos.__apellidos`, ¿no sería más correcto para querer obtener el valor de los apellidos de la clase Persona? Bueno, aunque pensemos esto, si utilizamos `__` igualmente dará el mismo error porque no se puede acceder desde fuera a una propiedad o método encapsulado.

```
print(Carlos.__apellidos)
Traceback (most recent call last):
  File "main.py", line 8, in <module>
    print(Carlos.__apellidos)
AttributeError: 'Persona' object has no attribute '__apellidos'
```

### ¿Cómo podemos acceder o modificar las variables, propiedades, o los métodos de ámbito privado?

Tendremos que crear métodos específicos que puedan acceder a esas variables, propiedades o métodos.

```
class A:
# Constructor de clase
  def __init__(self):

  # Asignamos 20 a esta propiedad privada
    self.__propiedad = 20

  def __metodo(self):
    print("Soy un método privado.")

  # Soy un método público que leerá y ejecutará contenido privado.
  def mostrar(self):
    self.__metodo()
    print(self.__variable)

  def cambiar(self,propiedad):
    self.__propiedad = propiedad
    print("Esta es la nueva propiedad %i % (self.__propiedad))

# Instanciamos el objeto
obj = A()

# Ejecutamos el método público mostrar()
obj.mostrar()

# Modificamos el valor propiedad
obj.cambiar(300)
```

## Polimorfismo

Es la capacidad que tiene un objeto para ser y poder ser otra cosa al mismo tiempo. Por ejemplo, un pájaro. Un pájaro puede ser un pingüino y un gorrión, ambos tienen propiedades en común como las patas, ojos, orejas; el color de las plumas, de los ojos, de los picos. También, tienen una serie de métodos similares como volar, poner huevos, comer, dormir… ¿Qué tienen en común todos ellos? Que son pájaros. Por lo tanto, un pájaro puede ser un gorrión o puede ser un pingüino al mismo tiempo sin perder lo que es su esencia, que es ser un pájaro.

```
# Creamos la clase Pájaro
class Pajaro:
 
  # Método volar
  def nadar(self):
    print("Puedo nadar.")
 
  def volar(self):
    print("Puedo volar.")

class Pinguino(Pajaro):
  def nadar(self):
    print("Puedo nadar.")

  def volar(self):
    print("No puedo volar.")
 
  def ver_volar(birds)
    birds.volar()

gorrion=Pajaro()
pinguino=Pinguino()

# Este imprimirá que pude volar
ver_volar(gorrion)

# Este imprimirá que no puede volar
ver_volar(pinguino)
```