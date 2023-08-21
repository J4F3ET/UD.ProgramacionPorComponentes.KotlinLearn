# Resumen capítulo 2
## Indice
1. [Variables](#variables)
2. [Funciones](#funciones)
3. [Expresiones y Instrucciones en kotlin](#expresiones-y-instrucciones-en-kotlin)
4. [Clases y propiedades](#clases-y-propiedades)
5. [Estructura when](#estructura-when)
6. [Cast en Kotlin](#cast-en-kotlin)
7. [Bucles(loops)](#buclesloops)
8. [Rangos](#rangos)
9. [Exportar e importar](#exportar-e-importar)
10. [Excepciones (Try catch)](#excepciones-try-catch)
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
