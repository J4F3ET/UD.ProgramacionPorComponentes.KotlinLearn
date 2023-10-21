# Resumenes de Kotlin in action
## Indice
- [Capítulo 1](#resumen-capítulo-1)
- [Capítulo 2](#resumen-capítulo-2)
- [Capítulo 3](#resumen-capítulo-3)
- [Capítulo 4](#resumen-capítulo-4)
- [Capítulo 5](#resumen-capítulo-5)
# Resumen capítulo 1
## Indice
- [Kotlin](#kotlin)
- [Primeros pasos](#primeros-pasos-en-kotlin)
- [Funcional y orientado a objetos](#funcional-y-orientado-a-objetos)
- [Compilación en Kotlin](#compilación-en-kotlin)
## Kotlin
  Es un lenguaje similar a java y permite interpolar(poner Kotlin dentro de java) el código. La razón de Kotlin es buscar ser una alternativa
productiva,segura  y concisa a java. Una de las mayores fortalezas de Kotlin es la multiplataforma.
**Kotlin se puede compilar a JS** lo que permite ejecutar código en el navegador.
### Áreas de uso
- Backend
- Mobile
### Frameworks
- Exposed(ORM)
### Kotlin Backend (del lado del servidor)
Kotlin tiene muchas ventajas al ser un lenguaje nuevo en el mundo, puesto que los lenguajes legacy, necesitan de framework para diversas funcionalidades y hacer más productiva la elaboración de sistemas. Otras veces se necesita ampliar o hacerle mantenimiento a sistemas en dichos lenguajes (legacy). Kotlin cuenta con librerías que nos permiten implementar funciones que otros lenguajes no, o pues no sin la necesidad de una herramienta externa(framework)
```kotlin
  fun renderPersonList(persons: Collection<Person>) =
    createHTML().table {
      for (person in persons) {
        tr {
          td { +person.name }
          td { +person.age }
        }
      }
    }
```
## Primeros pasos en Kotlin
En java usamos `int a = null;` pero Kotlin nos presenta una nueva forma de crear variables `val a:int? = null` puede ser confuso pero el lo que se refieres `?` a que en algún momento la variable puede ser `null`.<br>
Kotlin es un lenguaje de tipado estático(el tipo de variable no cambia), pero es flexible al momento de declarar una variable, pues no es necesario decirle que tipo de dato va almacenar dicha variable
```kotlin
  data class person(
    val name:String
    val age:Int? = null
  )
  fun main(args: Array<String>) {
    val persons = listOf(
      Person("Alice"),
      Person("Bob", age = 29)
    )
    val oldest = persons.maxBy { it.age ?: 0 }
  }
```
La variable `persons` aloja los datos de la clase `person` pero en ningún momento le diga que clase de variable es **por su contexto Kotlin asumió el tipo de dato** lo mismo sucedió con la variable `oldest`

## Funcional y orientado a objetos
Imagina que tienes dos fragmentos de código similares que implementan una tarea similar (por ejemplo, buscar un elemento coincidente en una colección), pero difieren en los detalles (cómo se detecta el elemento coincidente). Puedes extraer fácilmente la parte común de la lógica en una función y pasar las partes diferentes como argumentos. Esos argumentos son en sí mismos funciones, pero puedes expresarlos usando una sintaxis concisa para funciones anónimas llamadas expresiones lambda
```kotlin
  fun findAlice() = findPerson { it.name == "Alice" }
  fun findBob() = findPerson { it.name == "Bob" }
```
`findPerson()` contiene la lógica general para encontrar a una persona y el bloque `{}` contiene la lógica para buscar a la persona en especifico
## Compilación en Kotlin
1. El código Kotlin se almacena en archivos con extensión `.kt`
2. Luego el compilador genera los archivos `.class`
3. Se empaquetan los `.class` y se compilan dependiendo del tipo de proyecto, aquí  es donde aparece el `.jar`.
   Ejemplo:
   ```php
   kotlinc <archivo o directorio fuente> -include-runtime -d <nombre del archivo JAR>
   ```
5. Luego se ejecuta
   ```php
   java -jar <nombre del archivo JAR>
   ```
6. Al momento de ejecutar el `Kotlin runtime` se ejecuta con las bibliotecas de Kotlin pues depende de ellas.
7. Al finalizar esta la aplicación
   Jemerov, D., & Isakova, S. (2017). "Título del prólogo." En A. Breslav (Ed.), Título del libro (14). Manning Publications Co
   ![image](https://github.com/J4F3ET/UD.ProgramacionPorComponentes.KotlinLearn/assets/104593574/9dbe29f6-cb10-413a-b737-7e32b68dba4e)
# Resumen capítulo 2
## Indice
- [Variables](#variables)
- [Funciones](#funciones)
- [Expresiones y Instrucciones en kotlin](#expresiones-y-instrucciones-en-kotlin)
- [Clases y propiedades](#clases-y-propiedades)
- [Estructura when](#estructura-when)
- [Cast en Kotlin](#cast-en-kotlin)
- [Bucles(loops)](#buclesloops)
- [Rangos](#rangos)
- [Exportar e importar](#exportar-e-importar)
- [Excepciones (Try catch)](#excepciones-try-catch)
## Variables
En java usamos `int a = null;` pero kotlin nos presenta una nueva forma de crear variables `val a:int? = null` puede ser confuso pero el lo que se refieres `?` a que en algún momento la variable puede ser `null`.<br>
Kotlin es un lenguaje de tipado estático(el tipo de variable no cambia), pero es flexible al momento de declarar una variable, pues no es necesario decirle que tipo de dato va almacenar dicha variable
```kotlin
  data class person(
    val name:String
    val age:Int? = null
  )
  fun main(args: Array<String>) {
    val persons = listOf(Person("Alice"),Person("Bob", age = 29))
    val oldest = persons.maxBy { it.age ?: 0 }
  }
```
La variable `persons` aloja los datos de la clase `person` pero en ningún momento le diga que clase de variable es **por su contexto Kotlin asumió el tipo de dato** lo mismo sucedió con la variable `oldest`
### Variables inmutables y mutables
- val (de value) - Referencia inmutable. Una variable declarada con "val" no puede ser reasignada después de inicializarse.
- var (de variable) - Referencia mutable. El valor de una variable de este tipo puede cambiarse.
## Funciones
Las funciones en Kotlin de declaran con `fun` seguido el nombre de la función, luego los parámetros con su tipo de dato `(param:Int)`y al final el tipo de valor que retornara `(param:Int):Int` de manera que la estructura(firma de la función) se vea así

```kotlin
  fun name(paramName: Int, paramName2: String):Int{
    logica de la función...
  }
```

## Expresiones y Instrucciones en kotlin
En Kotlin, el concepto de expresiones e instrucciones es importante porque afecta cómo funcionan ciertas estructuras y cómo se pueden usar en diferentes contextos.

- **Expresiones** son porciones de código que tienen un valor y pueden ser usadas en cualquier lugar donde se espere un valor. Por ejemplo, una suma (a + b) es una expresión que tiene un valor.

- **Instrucciones** son porciones de código que realizan una acción sin necesariamente tener un valor. Por ejemplo, una asignación (`a = 10`) es una instrucción, ya que simplemente asigna un valor a una variable sin retornar ningún valor en sí.

En Kotlin, el `if` se comporta como una **expresión**, lo que significa que tiene un valor y puede ser usado en contextos donde se espera un valor. Esto permite asignar el resultado de un `if` directamente a una variable o usarlo en otro cálculo.

Por ejemplo:
```kotlin
val x = if (condition) 10 else 20
```
En este caso, `x` tomará el valor 10 o 20 dependiendo de la condición. Esto es posible porque el `if` en Kotlin es una expresión que tiene un valor.

En contraste, en muchos otros lenguajes como Java, el `if` es una **instrucción**, lo que significa que no tiene un valor y no puede ser usado directamente para óes o en otros cálculos.
### Cuerpos de Expresiones
En kotlin se pueden simplificar funciones y no ponerle un cuerpo encerrado entre llaves, para lograr esto la función deberá de ser de una **expresión**

La siguiente función esta en la forma **"cuerpo de bloque"** por que posee `{}`
```kotlin
fun max(a: Int,b: Int): Int{
  return if(a > b) a else b
}
```
si se observa `if(a > b) a else b` es una **expresión** por ende se puede llevar a la forma **"cuerpo de expresión"** eliminando `{}` y asignando el valor de la expresión a la función con un `=` quedando de la siguiente forma.
```kotlin
fun max(a: Int, b: Int): Int = if (a > b) a else b
```
y se puede omitir el tipo de dato que retorna quedando
```kotlin
fun max(a: Int, b: Int) = if (a > b) a else b
```
## Clases y propiedades
Kotlin tiene algunas propiedades con respecto a las clases, para ver de mejor forma esto la mejor manera es comparando Kotlin con Java.
- Java
```java
/* Java */
public class Person {
  private final String name;

  public Person(String name) {
    this.name = name;
  }
  public String getName() {
    return name;
  }
}
```
- Kotlin
```kotlin
class Person(val name: String)
```
Kotlin tiene un sistema para generar getter y setter automáticos de los miembros de la clase

| Declaración                  | Getter     | Setter      | Visibilidad por defecto |
|-----------------------------|------------|-------------|-------------------------|
| `val propertyName: Type`    | Sí (Público) | No          | Pública                 |
| `var propertyName: Type`    | Sí (Público) | Sí (Público) | Pública                 |

Esta tabla resume cómo se generan los getters y setters en Kotlin:

- Cuando declaras una propiedad con `val`, se genera un getter público automáticamente, lo que permite acceder al valor de la propiedad desde cualquier lugar. No se genera un setter, ya que la propiedad es de solo lectura.

- Cuando declaras una propiedad con `var`, se generan tanto un getter público como un setter público automáticamente. Esto permite tanto leer como escribir el valor de la propiedad desde cualquier lugar.

Pero claro no estamos aplicando **buenas practicas** por ende debemos instancias los miembros de la clase con `private` esto afecta a la creación de getters y setters por ende tocaría crearlos similar a java.
```kotlin
class Perso(private val name: String){
  fun getName() = this.name
  fun setName(newName:String){
    this.name = newName
  }
}
```
### Implementar una interfaz
En kotlin se implementa una interfaz de la siguiente manera
```kotlin
class Button : Clickable {
  override fun click() = println("I was clicked")
}
```
Como se puede ver la clase `Button` implementa la interfaz `Clickable` y se sobrescribe el método `click()` con la palabra reservada `override` y se implementa la lógica del método.
### Personalización de accesorios
En algunos casos es posible que no se necesite añadir un `private` a un miembro de una clase y los getters y setters se usen con normalidad, se pueden editar o sobre escribir la lógica
```kotlin
class Rectangle(val height: Int, val width: Int) {
val isSquare: Boolean
get() = height == width
}
fun createRandomRectangle(): Rectangle {
val random = Random()
return Rectangle(random.nextInt(), random.nextInt())
}
```
La clase `Rectangle` se tiene el atributo `isSquare` con un valor Boolean, pero ¿como se define su valor?. En este caso el método `get() = height == width` define esa lógica para el getter del atributo `isSquare`

### Clase `data class`
Una `data class` en Kotlin es una clase especializada que se utiliza principalmente para representar datos de manera concisa y eficiente. Kotlin proporciona sintaxis y funcionalidades específicas para definir `data class`, lo que permite crear clases que automáticamente generan métodos estándar como `equals`, `hashCode`, `toString`, y más, basados en las propiedades declaradas en la clase.

Algunas de las características y ventajas clave de las `data class` son:

1. **Generación automática de métodos estándar:** Cuando defines una `data class`, Kotlin automáticamente genera los métodos `equals`, `hashCode`, `toString`, entre otros, basados en las propiedades declaradas. Esto es útil para comparar objetos y utilizarlos en colecciones.

2. **Desestructuración:** Puedes desestructurar una instancia de `data class` en varias variables individuales. Esto es especialmente útil para acceder a las propiedades de la clase de manera más conveniente.

3. **Copiado simplificado:** Kotlin proporciona el método `copy()` para crear una copia inmutable de una instancia de `data class` con la opción de modificar propiedades específicas.

4. **Comparación de contenido:** La implementación predeterminada de `equals` en una `data class` compara el contenido de las propiedades en lugar de la referencia del objeto, lo que es ideal para comparaciones de igualdad.

5. **Facilita la declaratividad:** Las `data class` permiten definir la estructura de tus datos de manera declarativa y expresiva.

6. **Beneficios en estructuras de datos:** Las `data class` son útiles para almacenar y manipular datos en estructuras como listas, conjuntos y mapas debido a su implementación automática de `equals` y `hashCode`.

Aquí tienes un ejemplo de cómo se declara y utiliza una `data class`:

```kotlin
data class Person(val name: String, val age: Int)

fun main() {
    val person1 = Person("Alice", 30)
    val person2 = Person("Bob", 25)

    println(person1) // Imprime: Person(name=Alice, age=30)
    println(person1 == person2) // Imprime: false

    val (name, age) = person1 // Desestructuración
    println("Name: $name, Age: $age") // Imprime: Name: Alice, Age: 30
}
```
### Clase `enum class`
Una enum class en Kotlin es una forma de definir un tipo de datos que representa un conjunto fijo de valores constantes. Estos valores se conocen como "miembros de la enumeración". Piensa en una enumeración como una lista predefinida de opciones o estados posibles.
```kotlin
enum class Color {
    RED, ORANGE, YELLOW, GREEN, BLUE, INDIGO, VIOLET
}
```
En esta enum class, `RED`, `ORANGE`, `YELLOW`, etc., son los miembros de la enumeración. Cada uno de estos miembros es una instancia única de la clase Color, que representa un color específico.

Una ventaja importante de usar enum class es que te permite tener un conjunto controlado de opciones y evitar errores tipográficos o valores inesperados. Además, puedes agregar propiedades y métodos a los miembros de la enumeración para hacerla más útil y rica en funcionalidad.

En resumen, una enum class en Kotlin es una manera conveniente y segura de definir un tipo de datos con un conjunto limitado y conocido de valores posibles.

## Estructura `When`
Se basaron en el sistema `Switch case` para idear la estructura `when`. Esta estructura es mas poderosa que un `Switch case` de java pues no tiene limitaciones con el objeto a comparar, puede ser un `Int`, `String`, `Boolean`, `Enum class` o cualquier otro objeto.Esta permite el manejo de manera mas versátil y concisa, podemos decir que es una **expresión** por ende trabaja similar a un `if` por eso se pueden hacer cosas como:
```kotlin
fun getMnemonic(color: Color) =
    when (color) {
        Color.RED -> "Richard"
        Color.ORANGE -> "Of"
        Color.YELLOW -> "York"
        Color.GREEN -> "Gave"
        Color.BLUE -> "Battle"
        Color.INDIGO -> "In"
        Color.VIOLET -> "Vain"
    }
println(getMnemonic(Color.BLUE))
```
```kotlin
>>> Battle
```
### Manejo de `when`
En kotlin con `when` podemos agrupar por grupos de valores, por ejemplo
```kotlin
fun getWarmth(color: Color) = when(color) {
RED, ORANGE, YELLOW -> "warm"
GREEN -> "neutral"
BLUE, INDIGO, VIOLET -> "cold"
}
```
le pasamos a `getMnemonic` un objeto `Color` para que evalué su `enumValue` que puede ser `RED,ORANGE,YELLOW,GREEN,BLUE,INDIGO,VIOLET` dependiendo su `enumValue` determina el valor que retornara en el caso `getMnemonic(color.BLUE)` retornara `Battle`

También se puede usar con otra clase de objetos o combinaciones de objetos
```kotlin
fun mix(c1: Color, c2: Color) =
  when (setOf(c1, c2)) {
    setOf(RED, YELLOW) -> ORANGE
    setOf(YELLOW, BLUE) -> GREEN
    setOf(BLUE, VIOLET) -> INDIGO
  else -> throw Exception("Dirty color")
}

println(mix(BLUE, YELLOW))
```
```kotlin
GREEN
```
Que hace `setOf()`. Crea un conjunto de colecciones y esto permite que no importe la combinación (a,b) o es (b,a) siempre retornara el mismo valor, pues lo considera un conjunto de colecciones igual.

Teniendo en cuenta la lógica del `setOf()`podemos crear conjuntos de colores por defecto y compararlos para determinar su **mix**

Algo más eficiente seria utilizare condicionales en vez de estar instanciando objetos solo para compararlos y retornar.
```kotlin
fun mixOptimized(c1: Color, c2: Color) =
when {
  (c1 == RED && c2 == YELLOW) || (c1 == YELLOW && c2 == RED) -> ORANGE
  (c1 == YELLOW && c2 == BLUE)|| (c1 == BLUE && c2 == YELLOW) -> GREEN
  (c1 == BLUE && c2 == VIOLET)||
  (c1 == VIOLET && c2 == BLUE) -> INDIGO
  else -> throw Exception("Dirty color")
}
println(mixOptimized(BLUE, YELLOW))
``````
```kotlin
GREEN
```
Si en `When` no se le pasa un argumento, se evalúa cada condición en cada rama y la primera rama que sea verdadera se ejecuta. Esto es similar a una se puede usar para evaluar una condición booleana.
## Cast en Kotlin
Para conocer la instancia de un objeto usamos `is` y para convertirlo usamos `as`. El `is` en java seria equivalente a un `intanceof` y el `as` a un `cast`
```kotlin
val n = e as Num
```
Por dentro Kotlin esta usando el `smart cast` que es un cast inteligente que solo se puede usar en variables que son inmutables, es decir que no cambian de valor
## Bucles(loops)
En kotlin se puede usar `for` y `while` de manera similar a java, pero con la diferencia que en kotlin se puede usar `for` para iterar sobre cualquier objeto que tenga un método `iterator()`
```kotlin
for (c in "abc") {
  print(c + 1)
}
```
el resto de bucles son similares a java
```kotlin
while (x > 0) {
  x--
}
```
```kotlin
do {
  val y = retrieveData()
} while (y != null)
```
## Rangos
En kotlin se puede usar rangos de manera similar a python, por ejemplo
```kotlin
for (i in 1..100) { ... } // 1..100 es un rango que incluye 100
for (i in 1 until 100) { ... } // 1..99 es un rango que no incluye 100
for (x in 2..10 step 2) { ... } // es un rango del 2 al 10 y que va de 2 en 2
for (x in 10 downTo 1) { ... } // es un rango del 10 al 1
if (x in 1..10) { ... } // verifica si x esta en el rango del 1 al 10
```
Nota: Los rangos son iterables, por lo que se pueden usar en bucles `for` y `when` también se pueden usar en `when` para verificar si un valor esta en un rango y por ultimo si kotlin se pueden hacer cosas como `"a"..."z"` que es un rango de caracteres de la `a` a la `z`
## Exportar e importar
En kotlin se puede exportar e importar de manera similar a java, pero con la diferencia que en kotlin se puede importar de manera mas especifica

En este ejemplo podemos ver como estamos importando un paquete completo
```kotlin
import ch02.colors.Color
```
mientras que en esta otra manera de importar solo estamos importando estamos importando los miembros de la clase `Color` que son `RED,ORANGE,YELLOW,GREEN,BLUE,INDIGO,VIOLET` a esto se le conoce como **importar explicita**
```kotlin
import ch02.colors.Color.*
```
## Excepciones (Try catch)
En Kotlin el manejo de excepciones es similar a java, pero con la diferencia que en kotlin no se necesita especificar que excepciones puede lanzar un método, es decir que no se necesita usar `throws` en la firma del método, por ejemplo
```kotlin
fun readNumber(reader: BufferedReader): Int? {
  try {
    val line = reader.readLine()
    return Integer.parseInt(line)
  } catch (e: NumberFormatException) {
    return null
  } finally {
    reader.close()
  }
}
```
como se puede ver en el ejemplo anterior no se especifica que excepción puede lanzar el método `readNumber` y en el `catch` se especifica el tipo de excepción que se quiere capturar, en este caso `NumberFormatException` y en el `finally` se cierra el `BufferedReader` que se le pasa como argumento al método `readNumber`

Kotlin tambien permite mas flexibilidad al momento de instanciar un objeto `Exception` y lanzarlo ya que no se necesita de un `new`, por ejemplo
```kotlin
if (porcentaje !in 0..100) {
    throw IllegalArgumentException(
        "Un valor de porcentaje debe estar entre 0 y 100: $porcentaje")
}
```
Pero Kotlin tiene sus diferencias en la manera de usar el `try catch` y es que en kotlin el `try catch` es una expresión, es decir que se puede usar en una asignación y si no tiene un cuerpo `{}` solo tomara como valor de retorno el ultimo valor de la expresión
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
# Resumen capítulo 4

## Indice

- [Interfaces y Clases Abstractas en Kotlin](#interfaces-clases-abstractas-y-clases-sealed)
- [Modificadores de Acceso y Modificadores de Herencia y Visibilidad](#modificadores-de-acceso-modificadores-de-herencia-y-visibilidad)
- [Clases internas y anidadas](#clases-internas-y-anidadas)
- [Constructores](#constructores)
- [Métodos Generados por el Compilador](#métodos-generados-por-el-compilador)

## Interfaces, clases abstractas y clases Sealed

En Kotlin, las interfaces son similares a las de Java 8. Pueden contener métodos abstractos y métodos con implementación predeterminada, pero no pueden tener estado.

Para declarar una interfaz en Kotlin, se utiliza la palabra clave `interface`. Las clases que implementan una interfaz deben proporcionar implementaciones para todos los métodos abstractos de la interfaz, utilizando la palabra clave `override`.

```kotlin
interface Clickable {
    fun click()
    fun showOff() = println("¡Soy clickable!")
}

class Button : Clickable {
    override fun click() = println("Fui clickeado")
}
```

En el ejemplo, `Clickable` es una interfaz que contiene dos métodos, uno abstracto (`click`) y otro con una implementación predeterminada (`showOff`). La clase `Button` implementa la interfaz y proporciona su propia implementación para el método `click`.

Cuando una clase implementa múltiples interfaces que tienen métodos con el mismo nombre, es necesario utilizar `super` con el nombre de la interfaz correspondiente para invocar una implementación específica.

```kotlin
class Button : Clickable, Focusable {
    override fun click() = println("Fui clickeado")
    override fun showOff() {
        super<Clickable>.showOff()
        super<Focusable>.showOff()
    }
}
```

En este caso, `Button` implementa tanto `Clickable` como `Focusable`, ambas con métodos `showOff`. La implementación de `showOff` en `Button` llama a ambas implementaciones heredadas utilizando `super`.

Las clases abstractas en Kotlin se declaran con la palabra clave `abstract`. Pueden contener métodos abstractos, que son declaraciones de métodos sin implementación. Las clases que heredan de una clase abstracta deben proporcionar implementaciones para todos los métodos abstractos.

### Clases Sealed

Sealed classes son una característica en Kotlin que permite definir jerarquías de clases restringidas. Esto es útil cuando tienes una jerarquía de clases donde quieres manejar todos los posibles subtipos en una expresión `when`, pero no quieres tener que agregar siempre una rama `else` por defecto. Las clases selladas son una forma de garantizar que solo los subtipos directos definidos en la clase sellada pueden existir.

Para definir una clase sellada, debes marcar la clase base con el modificador `sealed`. Luego, defines todos los subtipos directos como clases anidadas dentro de la clase base. Por ejemplo:

```kotlin
sealed class Expr {
    class Num(val value: Int) : Expr()
    class Sum(val left: Expr, val right: Expr) : Expr()
}
```

En este ejemplo, `Expr` es una clase sellada con dos subtipos directos: `Num` y `Sum`. Como estos subtipos están definidos dentro de la clase sellada, no pueden existir subtipos adicionales fuera de la clase `Expr`.

La ventaja clave de las clases selladas es que cuando utilizas una expresión `when` para manejar todos los subtipos, no necesitas proporcionar una rama `else` porque ya se sabe que solo hay un conjunto finito de subtipos:

```kotlin
fun eval(e: Expr): Int = when (e) {
    is Expr.Num -> e.value
    is Expr.Sum -> eval(e.left) + eval(e.right)
}
```

En este caso, no es necesario proporcionar una rama `else` porque todas las posibilidades están cubiertas por los subtipos de `Expr`.

Si intentas agregar un nuevo subtipo fuera de la clase sellada, el código no compilará, lo que te obligará a actualizar todas las ubicaciones donde se manejan los subtipos. Esto ayuda a prevenir errores sutiles que podrían ocurrir si olvidas manejar un nuevo subtipo.

En resumen, las clases selladas son útiles cuando quieres crear una jerarquía de clases con un conjunto limitado y conocido de subtipos, y deseas garantizar que todos los subtipos sean manejados explícitamente en las expresiones `when`.

## Modificadores de Acceso, Modificadores de Herencia y Visibilidad

En Kotlin, los modificadores de acceso y los modificadores de herencia desempeñan un papel fundamental en la construcción de jerarquías de clases y en la seguridad de los miembros de una clase. Aquí hay una breve descripción de estos modificadores junto con ejemplos en Kotlin:

### Modificadores de Acceso:

1. **public**: Predeterminado para miembros de clases. Los miembros públicos son accesibles desde cualquier lugar.

```kotlin
class MiClase {
    public val miVariable = 42
}
```

2. **internal**: Accesible dentro del módulo actual. Ideal para ocultar detalles de implementación de otros módulos.

```kotlin
internal class MiClaseInternal {
    internal val miVariable = 42
}
```

3. **protected**: Accesible solo dentro de la clase que los define y en sus subclases.

```kotlin
open class ClaseBase {
    protected val miVariable = 42
}

class SubClase : ClaseBase() {
    fun obtenerVariableBase(): Int {
        return miVariable // Acceso protegido permitido en subclase
    }
}
```

4. **private**: Solo accesible dentro de la clase que los define.

```kotlin
class MiClasePrivada {
    private val miVariable = 42
}
```

### Modificadores de Herencia:

1. **final**: Impide que una clase o método sea heredado o sobrescrito.

```kotlin
open class ClaseBase {
    final fun metodoFinal() {}
}

class SubClase : ClaseBase() {
    // Error: No se puede sobrescribir un método final
    // override fun metodoFinal() {}
}
```

2. **open**: Marca una clase o método como susceptible de ser heredado o sobrescrito. Debe usarse explícitamente.

```kotlin
open class ClaseBaseAbierta {
    open fun metodoAbierto() {}
}

class SubClaseAbierta : ClaseBaseAbierta() {
    override fun metodoAbierto() {
        // Sobrescribiendo el método abierto
    }
}
```

3. **abstract**: Usado en clases para definir métodos abstractos que deben implementarse en subclases.

```kotlin
abstract class ClaseAbstracta {
    abstract fun metodoAbstracto()
}
```

4. **override**: Marca una función o propiedad que está sobrescribiendo un miembro de una superclase o interfaz.

```kotlin
interface MiInterfaz {
    fun metodoInterfaz()
}

class MiClase : MiInterfaz {
    override fun metodoInterfaz() {
        // Implementando el método de la interfaz
    }
}
```

Estos modificadores son esenciales para controlar la visibilidad y el comportamiento de la herencia en Kotlin, lo que contribuye a escribir un código más seguro y estructurado.

### Modificadores de Visibilidad

En Kotlin, los modificadores de visibilidad te permiten controlar el acceso a las declaraciones en tu código. Los modificadores son similares a los de Java, incluyendo `public`, `protected` y `private`. Sin embargo, la diferencia principal es que en Kotlin, la visibilidad predeterminada es `public` en lugar de `package-private` como en Java. Además, Kotlin introduce el modificador `internal`, que significa "visible dentro de un módulo".

Aquí hay un ejemplo que muestra cómo funcionan estos modificadores:

```kotlin
internal open class TalkativeButton : Focusable {
    private fun yell() = println("Hey!")
    protected fun whisper() = println("Let's talk!")
}

fun TalkativeButton.giveSpeech() {
    yell() // Esto genera un error, ya que yell() es privado
    whisper()
}
```

En este ejemplo, `TalkativeButton` es una clase con modificador `internal`, lo que significa que solo es visible dentro del módulo en el que se encuentra. `yell()` es una función privada, por lo que solo es accesible dentro de la propia clase `TalkativeButton`. `whisper()` es una función protegida, lo que significa que solo es accesible desde `TalkativeButton` y sus subclases.

La función `giveSpeech()` intenta acceder a `yell()`, lo que genera un error de compilación ya que `yell()` es privada y no se puede acceder desde fuera de la clase. Esto demuestra cómo los modificadores de visibilidad en Kotlin garantizan un control preciso sobre el acceso a las declaraciones en tu código.

## Clases internas y anidadas

En Kotlin, al igual que en Java, puedes declarar una clase dentro de otra clase. Esto puede ser útil para encapsular una clase auxiliar o colocar el código más cerca de donde se usa. Sin embargo, en Kotlin, las clases anidadas no tienen acceso a la instancia de la clase externa a menos que lo solicites específicamente.

Para ilustrar por qué esto es importante, considera un escenario en el que deseas definir un elemento de vista (`View`) cuyo estado se puede serializar. Es posible que no sea fácil serializar una vista directamente, pero puedes copiar todos los datos necesarios a otra clase auxiliar. Supongamos que defines una interfaz `State` que implementa `Serializable`, y la interfaz `View` declara métodos `getCurrentState` y `restoreState` que se pueden usar para guardar y restaurar el estado de una vista.

```kotlin
interface State : Serializable

interface View {
    fun getCurrentState(): State
    fun restoreState(state: State) {}
}
```

Es conveniente definir una clase que guarde el estado de un botón en la clase `Button`. Aquí está cómo se podría hacer en Java:

```java
public class Button implements View {
    @Override
    public State getCurrentState() {
        return new ButtonState();
    }

    @Override
    public void restoreState(State state) { /*...*/ }

    public class ButtonState implements State { /*...*/ }
}
```

¿Cuál es el problema con este código? ¿Por qué obtienes una excepción `java.io.NotSerializableException` si intentas serializar el estado del botón declarado? Esto puede parecer extraño al principio: la variable que serializas es de tipo `ButtonState`, no de tipo `Button`.

Todo se aclara cuando recuerdas que en Java, cuando declaras una clase dentro de otra clase, esta última se convierte automáticamente en una clase interna (inner class). La clase `ButtonState` en el ejemplo almacena implícitamente una referencia a su clase externa `Button`. Esto explica por qué `ButtonState` no se puede serializar: `Button` no es serializable y la referencia a él rompe la serialización de `ButtonState`.

Para solucionar este problema en Java, necesitas declarar la clase `ButtonState` como estática (static). Declarar una clase anidada como estática elimina la referencia implícita desde esa clase a su clase externa.

En Kotlin, el comportamiento predeterminado de las clases anidadas es el opuesto al de Java: una clase anidada en Kotlin sin modificadores explícitos es igual a una clase anidada estática en Java. Para convertirla en una clase interna para que contenga una referencia a una clase externa, usas el modificador `inner`.

La sintaxis para hacer referencia a una instancia de una clase externa en Kotlin también difiere de Java. Escribes `this@Outer` para acceder a la clase externa desde la clase interna. Por ejemplo:

```kotlin
class Outer {
    inner class Inner {
        fun getOuterReference(): Outer = this@Outer
    }
}
```

## Constructores

En Kotlin, puedes declarar constructores para tus clases de dos maneras principales: el constructor primario y los constructores secundarios.

**Constructor primario:**
El constructor primario se define junto con la declaración de la clase principal. Puedes usarlo para inicializar propiedades y recibir parámetros al crear una instancia de la clase. Aquí tienes un ejemplo:

```kotlin
class User(val nickname: String)
```

En este caso, `User` es la clase, `val` indica que `nickname` es una propiedad y `nickname: String` es un parámetro del constructor primario. Cuando creas una instancia de la clase `User`, debes proporcionar un valor para `nickname`.

**Constructores secundarios:**
Los constructores secundarios se definen en la clase con la palabra clave `constructor`. Puedes tener múltiples constructores secundarios en una clase. Estos son útiles cuando necesitas proporcionar diferentes formas de inicializar un objeto. Aquí hay un ejemplo:

```kotlin
class User(val nickname: String) {
    constructor(email: String, password: String) : this(email.split("@")[0])
}
```

En este ejemplo, `User` tiene un constructor primario que toma un `nickname`. Luego, se define un constructor secundario que toma un `email` y un `password`. Este constructor secundario llama al constructor primario con un valor derivado del `email`.

Puedes tener múltiples constructores secundarios con diferentes parámetros o diferentes lógica de inicialización según tus necesidades.

**Valores predeterminados en los parámetros del constructor:**
Tanto en el constructor primario como en los secundarios, puedes proporcionar valores predeterminados para los parámetros. Esto significa que puedes tener parámetros opcionales que no necesitas proporcionar al crear una instancia de la clase si no quieres cambiar sus valores predeterminados. Por ejemplo:

```kotlin
class User(val nickname: String, val isSubscribed: Boolean = true)
```

En este caso, `isSubscribed` tiene un valor predeterminado de `true`, por lo que si creas un usuario sin especificar `isSubscribed`, se asumirá que está suscrito.

## Métodos Generados por el Compilador

En Kotlin, puedes aprovechar el compilador para generar automáticamente métodos comunes como `equals`, `hashCode` y `toString`, lo que simplifica el manejo de clases de datos y la delegación de métodos. A continuación, se describen algunos de estos conceptos:

**Métodos Universales del Objeto: toString()**

- El método `toString()` permite obtener una representación de cadena de un objeto y es útil para depuración y registro.
- Puedes sobrescribir `toString()` en una clase para proporcionar una representación personalizada del objeto.
- Usar `toString()` proporciona información útil cuando imprimes objetos.

**Igualdad de Objetos: equals()**

- Puedes definir cómo se comparan dos objetos de una clase en función de tus necesidades.
- El método `equals()` te permite especificar si dos objetos deben considerarse iguales.
- Al comparar objetos personalizados, sobrescribe `equals()` para determinar la igualdad según las propiedades relevantes.

**HashCode: hashCode()**

- El método `hashCode()` calcula un valor numérico que representa un objeto.
- Dos objetos iguales deben tener el mismo valor de hash.
- Si sobrescribes `equals()`, también debes sobrescribir `hashCode()` para mantener la consistencia.

**Clases de Datos: data class**

- Las clases de datos son una característica especial de Kotlin para definir clases cuyo único propósito es almacenar datos.
- Al marcar una clase con `data`, el compilador genera automáticamente `equals`, `hashCode` y `toString` basados en las propiedades de la clase.
- Las clases de datos simplifican la creación y el manejo de objetos de datos inmutables.

**Delegación de Clases: by**

- Kotlin permite delegar la implementación de una interfaz o clase a otra clase mediante la palabra clave `by`.
- Esto evita la necesidad de repetir código y facilita la reutilización.
- Puedes usar la delegación de clases para crear composiciones de objetos y mejorar la modularidad.

**Companion Objects: Un Lugar para Métodos de Fábrica y Miembros Estáticos**

- En Kotlin, no hay miembros estáticos como en Java. En su lugar, se utilizan funciones de nivel superior y objetos compañeros (companion objects).
- Un objeto compañero (companion object) se declara dentro de una clase y se utiliza para definir métodos de fábrica y otros miembros estáticos.
- Los objetos compañeros pueden acceder a los miembros privados de la clase que los contiene.
- Los objetos compañeros pueden implementar interfaces y ser utilizados para crear instancias de la clase que los contiene.

**Extensiones de Objetos Compañeros (Companion-Object Extensions)**

- Las extensiones de objetos compañeros permiten definir métodos que se pueden llamar en la clase misma, como si fueran miembros estáticos.
- Se definen extensiones de objetos compañeros para un objeto compañero específico de una clase.
- Estas extensiones permiten una separación más limpia de las preocupaciones en el código y la reutilización de objetos en diferentes módulos.

**Expresiones de Objetos (Object Expressions)**

- Las expresiones de objetos permiten crear objetos anónimos sin necesidad de nombrarlos.
- Son útiles para crear implementaciones de interfaces o clases abstractas de manera concisa.
- Las expresiones de objetos pueden acceder a variables locales y modificarlas.

# Resumen capítulo 5
## Indice
- [Introducción a las lambdas en Kotlin](#introducción-a-las-lambdas-en-kotlin)
- [Sintaxis de las lambdas](#sintaxis-de-las-lambdas)
- [Variables capturadas por una lambda](#variables-capturadas-por-una-lambda)
  - [Clase de envoltura](#clase-de-envoltura)
- [Interfaces funcionales de Java en Kotlin](#interfaces-funcionales-de-java-en-kotlin)
- [Lambdas y colecciones](#lambdas-y-colecciones)
- [Lambdas con receptores](#lambdas-con-receptores)

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

