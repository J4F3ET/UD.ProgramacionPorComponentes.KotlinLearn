# Resumen capítulo 3

## Indice

- [Collections](#collections)
- [Valores por defecto para parámetros de funciones](#valores-por-defecto-para-parámetros-de-funciones)
- [Funciones de nivel superior](#funciones-de-nivel-superior)
- [Funciones de extensión](#funciones-de-extensión)
- [Override](#override)
- [varargs, infix y desestructuración](#varargs-infix-y-desestructuración)
- [Funciones animadas](#funciones-animadas)

## Collections

En Kotlin el crear una clase Collection es diferente en la sintaxis a Java pero en esencia es el mismo Java puesto que Kotlin no tiene su propia implementación de Collection, sino que usa la de Java.

```kotlin
  val set = hashSetOf(1, 7, 53)
  val list = arrayListOf(1, 7, 53)
  val map = hashMapOf(1 to "one", 7 to "seven", 53 to "fifty-three")
```

En el ejemplo anterior se crean tres colecciones diferentes, pero en el fondo son colecciones de Java. La diferencia es que en Kotlin se usa una sintaxis más concisa para crearlas. En el archivo [Estructuras de datos](./EstructurasDeDatos.md) podemos ver más a detalle las colecciones en Kotlin y sus casos de uso. Estas estructuras de datos son las Iterable de Java.

En algunos casos se necesitan modificar colecciones para alguna situación. Por ejemplo si necesitamos exportar los datos a un `csv` para guardarlo en un archivo o hacer análisis de datos. En ese caso podremos usar una funcion como `joinToString()` que nos permite convertir una colección en una cadena de texto.

```kotlin
    fun <T> joinToString(
        collection: Collection<T>,
        separator: String ,
        prefix: String,
        postfix: String
    ): String {
        val result = StringBuilder(prefix)
        for ((index, element) in collection.withIndex()) {
            if (index > 0) result.append(separator)
                result.append(element)
        }
        result.append(postfix)
        return result.toString()
    }
```

Los parametros de la función son:

- `collection`: La colección que se va a convertir a cadena de texto.
- `separator`: El separador que se usará entre los elementos de la colección.
- `prefix`: El prefijo que se usará al inicio de la cadena de texto.
- `postfix`: El sufijo que se usará al final de la cadena de texto.

```kotlin
  val list = listOf(1, 2, 3)
  println(list.joinToString(separator = "; ", prefix = "(", postfix = ")"))
```

El resultado de la función anterior sería `(1; 2; 3)`.

### Consejo

Kotlin recomienda seguir unas buenas practicas a la hora de usar funciones que pueden ser confusas a futuro. Por ejemplo el usar comentarios al momento de enviar parámetros a una función permite tener mas contexto.

Si vemos la siguiente función se entenderá mejor la idea

```kotlin
list.joinToString("; ","(",")")
```

En el ejemplo anterior no se sabe que es cada parámetro, pero si se usa un comentario se puede entender mejor

```kotlin
list.joinToString(/*separador*/"; ", /*prefijo */"(", /*sufijo*/")")
```

Otra buena practica es usar nombres de parámetros en las funciones. Esto permite que el código sea más legible y se entienda mejor(usar ingles para desarrollar cualquier aplicación es un estándar que ayuda a futuro el mantenimiento del proyecto).

```kotlin
list.joinToString(separator = "; ", prefix = "(", postfix = ")")
```

## Valores por defecto para parámetros de funciones

En Kotlin se pueden definir valores por defecto para los parámetros de una función. Esto permite que al momento de llamar la función no sea necesario enviar todos los parámetros, sino que se puede enviar solo los que se necesiten.

```kotlin
fun <T> joinToString(
    collection: Collection<T>,
    separator: String = ", ",
    prefix: String = "",
    postfix: String = ""
): String {
    val result = StringBuilder(prefix)
    for ((index, element) in collection.withIndex()) {
        if (index > 0) result.append(separator)
            result.append(element)
    }
    result.append(postfix)
    return result.toString()
}
```

En el ejemplo anterior se definen valores por defecto para los parámetros de la función `joinToString()`. Esto permite que al momento de llamar la función no sea necesario enviar todos los parámetros, sino que se puede enviar solo los que se necesiten.

```kotlin
val list = listOf(1, 2, 3)
println(list.joinToString())
```

El resultado de la función anterior sería `1, 2, 3`.

#### Nota:

En Java no existe este concepto de valores por defecto para los parámetros de una función. En Java se puede lograr el mismo resultado usando sobrecarga de funciones.

## Funciones de nivel superior

En kotlin existen funciones que no necesitan estar dentro de una clase, sino que pueden estar en el mismo nivel que las clases. Estas funciones se llaman funciones de nivel superior.

```kotlin
fun sumar(a: Int, b: Int): Int {
    return a + b
}

fun main() {
    val resultado = sumar(5, 3)
    println("El resultado de la suma es: $resultado")
}
```

Se puede ver que la función `sumar()`esta en el mismo nivel que la clase `main()`. Esto es posible en Kotlin, pero no en Java. No tuvimos que crear clases para las dos funciones

Por dentro Kotlin convierte las funciones de nivel superior en funciones estáticas de una clase. Esto permite que Kotlin sea compatible con Java.

En java el código anterior se vería así:

```java
public final class MainKt {
   public static final int sumar(int a, int b) {
      return a + b;
   }

   public static final void main() {
      int resultado = sumar(5, 3);
      String var2 = "El resultado de la suma es: " + resultado;
      System.out.println(var2);
   }
}
```

Si queremos cambiar el nombre de la clase que se genera en Java podemos usar la anotación `@JvmName` para indicarle a Kotlin que nombre usar.

```kotlin
@file:JvmName("NombreDeLaClase")
```

### Propiedades o Variables de nivel superior

En Kotlin también se pueden declarar variables de nivel superior. Estas variables se declaran fuera de una clase y se pueden usar en cualquier parte del código.

```kotlin
val PI = 3.1416
val nombre = "Juan"
```

En Java el código anterior se vería así:

```java
public final class MainKt {
   private static final double PI = 3.1416;
   private static final String nombre = "Juan";
}
```

De la misma manera en Kotlin usara estas Variables y las adicionara a una clase estática.

## Funciones de extensión

En Kotlin se pueden agregar funciones a una clase sin necesidad de modificar la clase. Esto se logra usando funciones de extensión.

```kotlin
Class Persona{
  var nombre:String
  var edad:Int
}
```

Queremos agregar una función a la clase `Persona` que nos permita saber si la persona es mayor de edad pero no podemos modificar la clase `Persona`. En este caso podemos usar una función de extensión.

```kotlin
fun Persona.esMayorDeEdad() = this.edad >= 18
```

De esa manera podemos usar la función `esMayorDeEdad()` en cualquier objeto de la clase `Persona`.

Estas funciones tiene sus limites, no podemos acceder a los atributos privados de la clase. Esto nos permite mantener el principio de encapsulamiento.

Tampoco podemos usar de manera global las funciones de extensión. Estas funciones solo se pueden usar en el archivo donde se declaran o en los archivos

### Importar funciones de extensión

Para importar una función de extensión se usa la palabra reservada `import` y se agrega el nombre del archivo donde se encuentra la función de extensión.

```kotlin
import NombreDelArchivo.funcionDeExtension
```

También se pueden importar todas las funciones de extensión de un archivo usando el operador `*`.

```kotlin
import NombreDelArchivo.*
```

o también cambiar el nombre de la función de extensión al momento de importarla.

```kotlin
import NombreDelArchivo.funcionDeExtension as nombreDeLaFuncion
```

## Override

En Kotlin se pueden sobrescribir funciones de una clase padre en una clase hija. Esto se logra usando la palabra reservada `override`.

```kotlin
 class View {
    open fun click() = println("View clicked")
}
 class Button : View() {
    override fun click() = println("Button clicked")
}
```

Si creamos un objeto tipo `Button` y llamamos la función `click()` se ejecutara la función de la clase `Button` y no la de la clase `View`.

```kotlin
fun main() {
    val view: View = Button()
    view.click()
}
```

El resultado de la función anterior sería `Button clicked`.

#### Nota:

Si la clase tiene una función miembro con la misma firma que una función de extensión, la función miembro siempre tiene prioridad.

## varargs, infix y desestructuración

Kotlin tiene algunas características que no existen en Java. Estas características son:

1. **La palabra clave `vararg`**: Esta palabra clave te permite declarar una función que puede recibir un número variable de argumentos del mismo tipo. Es especialmente útil cuando deseas pasar múltiples valores a una función sin tener que empaquetarlos en un arreglo o lista antes. Por ejemplo:

```kotlin
fun printNumbers(vararg numbers: Int) {
    for (number in numbers) {
        println(number)
    }
}

printNumbers(1, 2, 3) // Imprime: 1 2 3
```

- Con un `*` se puede desempaquetar listas o arrays para mandarlos como argumentos de una función.

```kotlin
val list = listOf(1, 2, 3)
printNumbers(*list.toIntArray()) // Imprime: 1 2 3
```

2. **Notación infija**: En Kotlin, puedes usar funciones de un solo argumento en una forma más concisa, conocida como notación infija. Esto significa que puedes omitir el punto y los paréntesis cuando llamas a estas funciones. Por ejemplo:

```kotlin
infix fun Int.times(str: String) = str.repeat(this)

println(3 times "Hola ") // Imprime: Hola Hola Hola
```

3. **Declaraciones de desestructuración**: En ocasiones, es posible que desees desempaquetar los elementos de una estructura de datos en múltiples variables. Las declaraciones de desestructuración te permiten hacer precisamente eso. Por ejemplo:

```kotlin
val (name, age) = person // Suponiendo que person es un objeto con propiedades name y age
println("$name tiene $age años")
```

## Funciones animadas

En kotlin te permite crear funciones dentro de otras funciones con el fin de eliminar código repetitivo

```kotlin
class User(val id: Int, val name: String, val address: String)
fun saveUser(user: User) {
    if (user.name.isEmpty()) {
        throw IllegalArgumentException(
        "Can't save user ${user.id}: empty Name")
    }
    if (user.address.isEmpty()) {
        throw IllegalArgumentException(
        "Can't save user ${user.id}: empty Address")
    }
    // Save user to the database
}
>>> saveUser(User(1, "", ""))
java.lang.IllegalArgumentException: Can't save user 1: empty Name
```

Se ve algo repetitivo el codigo anterior, para evitar esto se puede crear una funcion dentro de la funcion `saveUser()` que valide los campos de la clase `User`.

```kotlin
fun saveUser(user: User) {
    fun validate(user: User,
        value: String,
        fieldName: String){
        if (value.isEmpty()) {
            throw IllegalArgumentException(
            "Can't save user ${user.id}: empty $fieldName")
        }
    }
    validate(user, user.name, "Name")
    validate(user, user.address, "Address")
    // Save user to the database
}
```
