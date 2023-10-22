# Resumen capítulo 6
## Indice
- [Tipos básicos en Kotlin](#tipos-básicos-en-kotlin)
- [Nullabilidad en Kotlin](#nullabilidad-en-kotlin)
- [El operador Elvis](#el-operador-elvis)
- [Funciones de extensión y tipos anulables](#funciones-de-extensión-y-tipos-anulables)
- [Clases selladas](#clases-selladas)
- [Delegación de propiedades](#delegación-de-propiedades)
- [Delegación de clases](#delegación-de-clases)
- [Delegación de interfaces](#delegación-de-interfaces)
- [Delegación de funciones](#delegación-de-funciones)
## Tipos básicos en Kotlin
- Tipos enteros: Byte, Short, Int y Long.
- Tipos de números de punto flotante: Float y Double.
- Tipo de carácter: Char.
- Tipo booleano: Boolean.

A diferencia de Java, Kotlin no diferencia entre tipos primitivos y tipos de referencia. En Kotlin, todos los tipos son objetos, lo que significa que se pueden llamar métodos y propiedades en ellos. Además, Kotlin tiene una sintaxis más concisa para declarar variables y constantes.

Por ejemplo, para declarar una variable entera en Kotlin, se puede escribir:

```Kotlin
val edad: Int = 25
```

Esto declara una variable llamada `edad` de tipo Int con un valor de 25. La palabra clave `val` indica que la variable es de solo lectura, lo que significa que no se puede cambiar después de su inicialización.

Otro ejemplo es la declaración de una variable booleana:

```Kotlin
var esMayorDeEdad: Boolean = true
```

Esto declara una variable llamada `esMayorDeEdad` de tipo Boolean con un valor de verdadero. La palabra clave `var` indica que la variable es mutable, lo que significa que se puede cambiar su valor más adelante en el código.

## Nullabilidad en Kotlin
En Kotlin, se pueden declarar tipos de datos como nulos o no nulos. Esto significa que se puede indicar explícitamente si una variable puede contener un valor nulo o no.

Por ejemplo, para declarar una variable que puede ser nula, se puede escribir:

```Kotlin
var nombre: String? = null
```

Esto declara una variable llamada `nombre` de tipo String que puede ser nula. La pregunta `?` después del tipo indica que la variable puede ser nula. Si se intenta acceder a una variable nula, se producirá un error en tiempo de compilación.

Para trabajar con variables nulas en Kotlin, se puede utilizar el operador de llamada segura `?.` que permite llamar a métodos o acceder a propiedades de una variable nula sin producir un error en tiempo de ejecución. Por ejemplo:

```Kotlin
val longitudNombre: Int? = nombre?.length
```

Esto declara una variable llamada `longitudNombre` de tipo Int que puede ser nula. Si `nombre` es nulo, la expresión se evalúa como nula y no se produce un error en tiempo de ejecución.
## El operador Elvis
El operador Elvis es un operador que permite proporcionar un valor predeterminado en caso de que una variable sea nula. El operador se escribe como `?:` y se utiliza en una expresión que tiene dos valores posibles: el valor de la variable o un valor predeterminado.

Por ejemplo, para asignar un valor predeterminado a una variable nula, se puede escribir:

```Kotlin
val nombre: String? = null
val nombreNoNulo: String = nombre ?: `Desconocido`
```

En este ejemplo, la variable `nombre` es nula, por lo que se utiliza el valor predeterminado `Desconocido` en la variable `nombreNoNulo`. Si `nombre` no fuera nulo, se utilizaría su valor en lugar del valor predeterminado.

El operador Elvis también se puede utilizar en combinación con el operador de llamada segura `?.` para proporcionar un valor predeterminado en caso de que una variable sea nula. Por ejemplo:

```Kotlin
val longitudNombre: Int = nombre?.length ?: 0
```

En este ejemplo, la variable `nombre` puede ser nula, por lo que se utiliza el operador de llamada segura `?.` para acceder a su propiedad `length`. Si `nombre` es nulo, se utiliza el valor predeterminado `0` en la variable `longitudNombre`.

## Funciones de extensión y tipos anulables
Las funciones de extensión son funciones que se pueden agregar a una clase existente sin modificar su código fuente. Esto permite extender la funcionalidad de una clase sin tener que crear una subclase o modificar la clase original.

En Kotlin, se pueden declarar funciones de extensión para tipos anulables. Esto significa que se pueden llamar funciones en variables que pueden ser nulas sin producir un error en tiempo de ejecución. Para declarar una función de extensión para un tipo anulable, se utiliza el operador `?` después del nombre del tipo.

Por ejemplo, para declarar una función de extensión que comprueba si una cadena es nula o está en blanco, se puede escribir:

```Kotlin
fun String?.isNullOrBlank(): Boolean =
    this == null || this.isBlank()
```

En este ejemplo, la función `isNullOrBlank` es una función de extensión para el tipo String anulable. La función comprueba si la cadena es nula o está en blanco y devuelve un valor booleano.

Para llamar a una función de extensión en una variable anulable, se utiliza la sintaxis de llamada segura `?.` para evitar errores en tiempo de ejecución. Por ejemplo:

```Kotlin
val nombre: String? = null
val esNombreVacio = nombre.isNullOrBlank()
```

En este ejemplo, la variable `nombre` es nula, pero la función de extensión `isNullOrBlank` se puede llamar sin producir un error en tiempo de ejecución gracias al operador de llamada segura `?.`.
## Clases selladas
Las clases selladas son una característica de Kotlin que permite definir un conjunto limitado de subclases para una clase. Esto se logra mediante la palabra clave `sealed` antes de la definición de la clase.

Por ejemplo, para definir una clase sellada que representa diferentes tipos de operaciones matemáticas, se puede escribir:

```Kotlin
sealed class OperacionMatematica {
    class Suma(val a: Int, val b: Int) : OperacionMatematica()
    class Resta(val a: Int, val b: Int) : OperacionMatematica()
    class Multiplicacion(val a: Int, val b: Int) : OperacionMatematica()
    class Division(val a: Int, val b: Int) : OperacionMatematica()
}
```

En este ejemplo, la clase `OperacionMatematica` es una clase sellada que tiene cuatro subclases: `Suma`, `Resta`, `Multiplicacion` y `Division`. Cada subclase tiene dos propiedades `a` y `b` que representan los operandos de la operación.

Las clases selladas son útiles cuando se desea definir un conjunto limitado de subclases para una clase y se desea que todas las subclases sean conocidas en tiempo de compilación. Esto permite utilizar la exhaustividad de las expresiones `when` para manejar todos los casos posibles de una clase sellada.

Por ejemplo, para manejar todas las posibles operaciones matemáticas definidas en la clase sellada anterior, se puede escribir:

```Kotlin
fun calcular(op: OperacionMatematica): Int =
    when (op) {
        is OperacionMatematica.Suma -> op.a + op.b
        is OperacionMatematica.Resta -> op.a - op.b
        is OperacionMatematica.Multiplicacion -> op.a * op.b
        is OperacionMatematica.Division -> op.a / op.b
    }
```

En este ejemplo, la función `calcular` toma una instancia de la clase sellada `OperacionMatematica` y utiliza una expresión `when` para manejar todos los casos posibles de la clase sellada.

## Delegación de propiedades
 En Kotlin, la delegación de propiedades es una característica que permite delegar la implementación de una propiedad a otro objeto. Esto se logra mediante la palabra clave `by` seguida del objeto delegado.

Por ejemplo, para delegar la implementación de una propiedad `nombre` a otro objeto `Persona`, se puede escribir:

```Kotlin
class Persona(val nombreCompleto: String)

class Usuario(private val persona: Persona) {
    val nombre: String by persona::nombreCompleto
}
```

En este ejemplo, la clase `Usuario` tiene una propiedad `nombre` que está delegada a la propiedad `nombreCompleto` de la clase `Persona`. La propiedad `nombre` se puede acceder como si fuera una propiedad normal, pero su implementación está delegada al objeto `Persona`.

La delegación de propiedades también se puede utilizar para implementar propiedades calculadas. Por ejemplo, para implementar una propiedad `edad` que se calcula a partir de la fecha de nacimiento de una persona, se puede escribir:

```Kotlin
import java.time.LocalDate
import java.time.Period

class Persona(val fechaNacimiento: LocalDate)

class Usuario(private val persona: Persona) {
    val edad: Int by lazy {
        Period.between(persona.fechaNacimiento, LocalDate.now()).years
    }
}
```

En este ejemplo, la clase `Usuario` tiene una propiedad `edad` que se calcula a partir de la fecha de nacimiento de la clase `Persona`. La propiedad `edad` se implementa como una propiedad calculada que utiliza la clase `Period` de Java para calcular la diferencia entre la fecha de nacimiento y la fecha actual.
## Delegación de clases
la delegación de clases es una característica que permite delegar la implementación de una clase a otro objeto. Esto se logra mediante la palabra clave `by` seguida del objeto delegado.

Por ejemplo, para delegar la implementación de una clase `MiClase` a otro objeto `OtraClase`, se puede escribir:

```Kotlin
interface MiInterface {
    fun miFuncion()
}

class OtraClase : MiInterface {
    override fun miFuncion() {
        println(`Implementación de miFuncion en OtraClase`)
    }
}

class MiClase : MiInterface by OtraClase()
```

En este ejemplo, la clase `MiClase` está delegando la implementación de la interfaz `MiInterface` a la clase `OtraClase`. La clase `MiClase` se comporta como si implementara directamente la interfaz `MiInterface`, pero su implementación está delegada a la clase `OtraClase`.

La delegación de clases también se puede utilizar para implementar patrones de diseño como el patrón Decorador. Por ejemplo, para implementar un decorador que agrega funcionalidad a una clase `Componente`, se puede escribir:

```Kotlin
interface Componente {
    fun operacion()
}

class ComponenteConcreto : Componente {
    override fun operacion() {
        println(`Operación en ComponenteConcreto`)
    }
}

class Decorador(private val componente: Componente) : Componente by componente {
    fun operacionAdicional() {
        println(`Operación adicional en Decorador`)
    }
}
```

En este ejemplo, la clase `Decorador` está decorando la implementación de la interfaz `Componente` de la clase `ComponenteConcreto`. La clase `Decorador` se comporta como si implementara directamente la interfaz `Componente`, pero su implementación está delegada a la clase `ComponenteConcreto`. Además, la clase `Decorador` agrega una operación adicional que no está presente en la interfaz `Componente`.
## Delegación de interfaces
La delegación de interfaces es una característica que permite delegar la implementación de una interfaz a otro objeto. Esto se logra mediante la palabra clave `by` seguida del objeto delegado.

Por ejemplo, para delegar la implementación de una interfaz `MiInterface` a otro objeto `OtraClase`, se puede escribir:

```Kotlin
interface MiInterface {
    fun miFuncion()
}

class OtraClase : MiInterface {
    override fun miFuncion() {
        println(`Implementación de miFuncion en OtraClase`)
    }
}

class MiClase : MiInterface by OtraClase()
```

En este ejemplo, la clase `MiClase` está delegando la implementación de la interfaz `MiInterface` a la clase `OtraClase`. La clase `MiClase` se comporta como si implementara directamente la interfaz `MiInterface`, pero su implementación está delegada a la clase `OtraClase`.

La delegación de interfaces también se puede utilizar para implementar patrones de diseño como el patrón Adaptador. Por ejemplo, para implementar un adaptador que adapta una interfaz `ViejaInterface` a una interfaz `NuevaInterface`, se puede escribir:

```Kotlin
interface ViejaInterface {
    fun viejaFuncion()
}

interface NuevaInterface {
    fun nuevaFuncion()
}

class ClaseVieja : ViejaInterface {
    override fun viejaFuncion() {
        println(`Implementación de viejaFuncion en ClaseVieja`)
    }
}

class Adaptador(private val claseVieja: ClaseVieja) : NuevaInterface {
    override fun nuevaFuncion() {
        claseVieja.viejaFuncion()
    }
}
```

En este ejemplo, la clase `Adaptador` está adaptando la implementación de la interfaz `ViejaInterface` de la clase `ClaseVieja` a la interfaz `NuevaInterface`. La clase `Adaptador` se comporta como si implementara directamente la interfaz `NuevaInterface`, pero su implementación está delegada a la clase `ClaseVieja`.
## Delegación de funciones
En Kotlin, la delegación de funciones se puede lograr mediante el uso de lambdas y funciones de orden superior.

Por ejemplo, para delegar la implementación de una función `miFuncion` a una lambda, se puede escribir:

```Kotlin
fun miFuncion(funcion: () -> Unit) {
    funcion()
}

miFuncion { println(`Implementación de miFuncion en lambda`) }
```

En este ejemplo, la función `miFuncion` toma como parámetro una lambda que no recibe argumentos y no devuelve nada. La implementación de la función `miFuncion` está delegada a la lambda que se pasa como argumento.

La delegación de funciones también se puede utilizar para implementar funciones de orden superior que toman otras funciones como parámetros. Por ejemplo, para implementar una función de orden superior `ejecutar` que toma una función como parámetro y la ejecuta varias veces, se puede escribir:

```Kotlin
fun ejecutar(funcion: () -> Unit, veces: Int) {
    repeat(veces) {
        funcion()
    }
}

ejecutar({ println("Implementación de función en ejecutar") }, 3)
```

En este ejemplo, la función de orden superior `ejecutar` toma como parámetros una función que no recibe argumentos y no devuelve nada, y un número entero que indica cuántas veces se debe ejecutar la función. La implementación de la función `ejecutar` está delegada a la función que se pasa como argumento.