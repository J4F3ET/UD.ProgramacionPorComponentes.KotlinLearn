# Resumen capítulo 5
## Indice
- [Introducción a las lambdas en Kotlin](#introducción-a-las-lambdas-en-kotlin)
- [Sintaxis de las lambdas](#sintaxis-de-las-lambdas)
- [Variables capturadas por una lambda](#variables-capturadas-por-una-lambda)
  - [Clase de envoltura](#clase-de-envoltura)
- [Interfaces funcionales de Java en Kotlin](#interfaces-funcionales-de-java-en-kotlin)
- [Lambdas y colecciones](#lambdas-y-colecciones)
- [Lambdas con receptores](#lambdas-con-receptores)
- [Conclusiones y próximos pasos](#conclusiones-y-próximos-pasos)

## Introducción a las lambdas en Kotlin
Las lambdas son pequeños bloques de código que se pueden pasar como argumentos a otras funciones. En lugar de declarar una función y pasar una instancia de esa función a otra función, se puede pasar directamente un bloque de código como parámetro. Las lambdas son útiles para extraer estructuras de código comunes en funciones de biblioteca, lo que hace que el código sea más conciso y fácil de leer. En Kotlin, las lambdas tienen una sintaxis clara y concisa, lo que las hace fáciles de usar y entender.
```Kotlin
val numbers = listOf(1, 2, 3, 4, 5)
val evenNumbers = numbers.filter { it % 2 == 0 }
```
En este ejemplo, `numbers` es una lista de números enteros y `evenNumbers` es una nueva lista que contiene solo los números pares de `numbers`. La función `filter` es una función de biblioteca que toma una lambda como argumento y devuelve una nueva lista que contiene solo los elementos que cumplen con la condición especificada en la lambda. En este caso, la lambda `{ it % 2 == 0 }` verifica si el número es par (es decir, si su resto al dividirlo por 2 es 0) y devuelve `true` si es así.
## Sintaxis de las lambdas
En Kotlin, las lambdas tienen una sintaxis clara y concisa. La sintaxis básica de una lambda es la siguiente:

```Kotlin
{ argumentos -> cuerpo de la lambda }
```

La parte de los argumentos es opcional y se puede omitir si la lambda no toma ningún argumento. El cuerpo de la lambda es una expresión o un bloque de código que se ejecuta cuando se llama a la lambda.

Por ejemplo, aquí hay una lambda que toma un argumento y devuelve el doble del valor del argumento:

```Kotlin
val double = { x: Int -> x * 2 }
```

En este caso, `x: Int` es la lista de argumentos de la lambda y `x * 2` es el cuerpo de la lambda. La lambda toma un número entero `x` como argumento y devuelve el doble de ese número.

También es posible usar la sintaxis de referencia de función para crear una lambda. Por ejemplo, aquí hay una lambda que toma un argumento y devuelve el cuadrado del valor del argumento:

```Kotlin
val square: (Int) -> Int = Int::times
```

En este caso, `Int::times` es una referencia a la función `times` de la clase `Int`. La lambda toma un número entero como argumento y devuelve el cuadrado de ese número.

## Variables capturadas por una lambda
En Kotlin, las lambdas pueden capturar variables del contexto en el que se definen. Esto significa que pueden acceder a variables locales y parámetros de la función que las contiene. Cuando una lambda captura una variable, se crea una referencia a esa variable y se almacena junto con la lambda.

Si la variable es inmutable (es decir, si su valor no cambia), la lambda puede acceder a su valor en cualquier momento. Pero si la variable es mutable (es decir, si su valor puede cambiar), la lambda solo puede acceder a su valor actual en el momento en que se llama. Si la variable cambia después de que se haya creado la lambda, la lambda seguirá haciendo referencia al valor anterior.

Para capturar una variable mutable en una lambda, se puede usar una clase de envoltura que almacena una referencia a la variable. Por ejemplo, aquí hay una lambda que captura una variable mutable `counter`:

```Kotlin
class Ref<T>(var value: T)

val counter = Ref(0)
val inc = { counter.value++ }
```

En este caso, la clase `Ref` es una clase de envoltura (una ) que almacena una referencia a una variable mutable. La variable `counter` es una instancia de la clase `Ref` que almacena un valor entero. La variable `inc` es una lambda que captura la variable `counter` y aumenta su valor en uno cada vez que se llama.

Es importante tener en cuenta que, aunque la variable capturada es mutable, la referencia a la variable que se almacena en la lambda es inmutable. Esto significa que la lambda no puede cambiar la referencia a la variable, pero puede cambiar el valor de la variable a través de la referencia almacenada.

### Clase de envoltura
Una clase de envoltura es una clase que almacena una referencia a un valor. La clase de envoltura puede ser mutable o inmutable. Si la clase de envoltura es mutable, el valor almacenado se puede cambiar. Si la clase de envoltura es inmutable, el valor almacenado no se puede cambiar.

Por ejemplo, aquí hay una clase envoltura simple que almacena un valor entero:

```Kotlin
class Ref<T>(var value: T)
```

En este caso, `Ref` es una clase genérica que almacena un valor de cualquier tipo `T`. La variable `value` es una propiedad de la clase que almacena el valor. La clase proporciona una interfaz para acceder y modificar el valor a través de esta propiedad.

Para utilizar esta clase envoltura para capturar una variable mutable en una lambda, se puede crear una instancia de la clase y pasarla como argumento a la lambda. Por ejemplo, aquí hay una lambda que captura una variable mutable `counter` utilizando la clase envoltura `Ref`:

```Kotlin
val counter = Ref(0)
val inc = { counter.value++ }
```
En este caso, `counter` es una instancia de la clase `Ref` que almacena un valor entero. La lambda `inc` captura la variable `counter` y la incrementa en uno cada vez que se llama, accediendo al valor a través de la propiedad `value` de la clase `Ref`.

## Interfaces funcionales de Java en Kotlin
En Java, una interfaz funcional es una interfaz que tiene exactamente un método abstracto. Estas interfaces se utilizan a menudo para representar funciones o acciones que se pueden pasar como argumentos a métodos o lambdas.

En Kotlin, las interfaces funcionales de Java se pueden utilizar de la misma manera que en Java. Esto significa que se pueden pasar como argumentos a métodos o lambdas, y se pueden implementar utilizando lambdas o clases anónimas.

Algunos ejemplos de interfaces funcionales de Java incluyen:

- `Runnable`: una interfaz que representa una acción que no toma argumentos ni devuelve un valor.
- `Callable`: una interfaz que representa una acción que toma argumentos y devuelve un valor.
- `Comparator`: una interfaz que representa una función que compara dos objetos y devuelve un valor entero que indica su orden relativo.

En Kotlin, se pueden utilizar estas interfaces funcionales de Java de la misma manera que en Java. Por ejemplo, aquí hay un ejemplo de cómo utilizar la interfaz `Runnable` de Java en Kotlin:

```Kotlin
val runnable = Runnable { println("Hello, world!") }
Thread(runnable).start()
```

En este caso, se crea una instancia de la interfaz `Runnable` utilizando una lambda que imprime "Hello, world!". Luego se crea un nuevo hilo de ejecución utilizando esta instancia de `Runnable`.

## Lambdas y colecciones
Las lambdas se utilizan a menudo en Kotlin para definir funciones que se pueden pasar como argumentos a estas funciones de extensión de colecciones. Por ejemplo, aquí hay un ejemplo de cómo utilizar una lambda para filtrar una lista de números:

```Kotlin
val numbers = listOf(1, 2, 3, 4, 5)
val evenNumbers = numbers.filter { it % 2 == 0 }
```

En este caso, la función `filter` es una función de extensión de la clase `List` que toma una lambda como argumento y devuelve una nueva lista que contiene solo los elementos que cumplen con la condición especificada en la lambda. La lambda en este caso es `{ it % 2 == 0 }`, que devuelve `true` si el número es par y `false` si es impar.

Además de `filter`, Kotlin proporciona una serie de otras funciones de extensión de colecciones que se pueden utilizar con lambdas, como `map`, `reduce`, `fold`, `forEach`, `groupBy`, `sortedBy`, y muchas más. Estas funciones se utilizan a menudo para realizar operaciones comunes en colecciones de datos de manera concisa y legible.

En Kotlin, existen varias funciones de extensión de colecciones que se pueden utilizar para manipular y transformar datos en colecciones. Algunos ejemplos de estas funciones incluyen:

- `filter`: devuelve una nueva colección que contiene solo los elementos que cumplen con una condición especificada en una lambda.
- `map`: devuelve una nueva colección que contiene los resultados de aplicar una función a cada elemento de la colección original.
- `reduce` / `fold`: combina los elementos de la colección en un solo valor utilizando una función especificada en una lambda.
- `forEach`: ejecuta una acción en cada elemento de la colección.
- `groupBy`: agrupa los elementos de la colección en subcolecciones basadas en una clave especificada en una lambda.
- `sortedBy`: devuelve una nueva colección ordenada según una clave especificada en una lambda.

Estas funciones se utilizan a menudo para realizar operaciones comunes en colecciones de datos de manera concisa y legible. Además, Kotlin también proporciona funciones de extensión adicionales para trabajar con colecciones, como `zip`, `flatten`, `distinct`, `partition`, y muchas más.

## Lambdas con receptores
Lambdas con receptores son una característica única de Kotlin que permite llamar métodos de un objeto diferente dentro del cuerpo de una lambda sin necesidad de calificarlos adicionalmente. En otras palabras, una lambda con receptor es una función anónima que se puede llamar como si fuera un método de un objeto específico.

La sintaxis para definir una lambda con receptor es la siguiente:

```Kotlin
val lambda: ReceiverType.() -> ReturnType = { /* lambda body */ }
```

En esta sintaxis, `ReceiverType` es el tipo de objeto que se utilizará como receptor dentro de la lambda, y `ReturnType` es el tipo de valor que devuelve la lambda. La lambda en sí se define dentro de las llaves y puede llamar a métodos del objeto receptor sin necesidad de calificarlos adicionalmente.

Por ejemplo, aquí hay un ejemplo de cómo utilizar una lambda con receptor para configurar una instancia de una clase:

```Kotlin
class Person {
    var name: String = ""
    var age: Int = 0
}

fun person(block: Person.() -> Unit): Person {
    val p = Person()
    p.block()
    return p
}

val person = person {
    name = "Alice"
    age = 30
}
```

En este caso, la función `person` toma una lambda con receptor que configura una instancia de la clase `Person`. Dentro de la lambda, se pueden llamar a los métodos `name` y `age` de la instancia de `Person` sin necesidad de calificarlos adicionalmente.

Las lambdas con receptores son una característica poderosa de Kotlin que se utilizan a menudo para crear DSL (Domain-Specific Languages) y para simplificar la configuración de objetos complejos.

