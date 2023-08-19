# Resumenes de Kotlin in action
## Indice
- [Capítulo 1](#resumen-capítulo-1)
- [Capítulo 2](#resumen-capítulo-2)
# Resumen capítulo 1
## Indice
- [Kotlin](#kotlin)
- [Primeros pasos](#primeros-pasos-en-kotlin)
- [Funcional y orientado a objetos](#funcional-y-orientado-a-objetos)
- [Compilación en Kotlin](#compilación-en-kotlin)
## Kotlin
Es un lenguaje similar a java y permite interpolar(poner kotlin dentro de java) el codigo. La razon de Kotlin es buscar ser una alternativa
productiva,segura  y concisa a java. Una de las mayores fortalezas de Kotlin es la multiplataforma.
**Kotlin se puede compilar a JS** lo que permite ejecutar codigo en el navegador.
### Areas de uso
- Backend
- Mobile
### Frameworks
- Exposed(ORM)
### Kotlin Backend (del lado del servidor)
Kotlin tiene muchas ventajas al ser un lenguaje nuevo en el mundo, puesto que los lenguajes legacy, necesitan de framework para diversas funcionalidades y hacer más productiva la elaboracion de sistemas. Otras veces se necesita ampliar o hacerle mantenimiento a sistemas en dichos lenguajes (legacy). Kotlin cuenta con librerias que nos permiten implementar funciones que otros lenguajes no, o pues no sin la necesidad de una herramienta externa(framework)
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
En java usamos `int a = null;` pero Kotlin nos presenta una nueva forma de crar variables `val a:int? = null` puede ser confuso pero el lo que se refieres `?` a que en algun momento la variable puede ser `null`.<br>
Kotlin es un lenguaje de tipado estatico(el tipo de variable no cambia), pero es flexible al momento de declarar una variable, pues no es necesario decirle que tipo de dato va almacenar dicha variable
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
La variable `persons` aloja los datos de la clase `person` pero en ningun momento le dige que clase de variable es **por su contexto Kotlin asumio el tipo de dato** lo mismo susedio con la variable `oldest`

## Funcional y orientado a objetos
Imagina que tienes dos fragmentos de código similares que implementan una tarea similar (por ejemplo, buscar un elemento coincidente en una colección), pero difieren en los detalles (cómo se detecta el elemento coincidente). Puedes extraer fácilmente la parte común de la lógica en una función y pasar las partes diferentes como argumentos. Esos argumentos son en sí mismos funciones, pero puedes expresarlos usando una sintaxis concisa para funciones anónimas llamadas expresiones lambda
```kotlin
  fun findAlice() = findPerson { it.name == "Alice" }
  fun findBob() = findPerson { it.name == "Bob" }
```
`findPerson()` contiene la lógica general para encontrar a una persona y el bloque `{}` contiene la logica para buscar a la persona en especifico
## Compilación en Kotlin
1. El codigo Kotlin se almacena en archivos con extensión `.kt`
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
Repositorio para repasar y aprender kotlin en base al libro "Kotlin in action".
## Indice
1. [Variables](#variables)
2. [Funciones](#funciones)
3. [Expresiones y Instrucciones en kotlin](#expresiones-y-instrucciones-en-kotlin)
4. [Clases y propiedades](#clases-y-propiedades)
5. [Estructura when](#estructura-when)
## Variables
En java usamos `int a = null;` pero kotlin nos presenta una nueva forma de crar variables `val a:int? = null` puede ser confuso pero el lo que se refieres `?` a que en algun momento la variable puede ser `null`.<br>
Kotlin es un lenguaje de tipado estatico(el tipo de variable no cambia), pero es flexible al momento de declarar una variable, pues no es necesario decirle que tipo de dato va almacenar dicha variable
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
La variable `persons` aloja los datos de la clase `person` pero en ningun momento le dige que clase de variable es **por su contexto Kotlin asumio el tipo de dato** lo mismo susedio con la variable `oldest`
### Variables inmutables y mutables
- val (de value) - Referencia inmutable. Una variable declarada con "val" no puede ser reasignada después de inicializarse.
- var (de variable) - Referencia mutable. El valor de una variable de este tipo puede cambiarse.
## Funciones
Las funciones en Kotlin de declaran con `fun` seguido el nombre de la funcion, luego los parametros con su tipo de dato `(param:Int)`y al final el tipo de valor que retornara `(param:Int):Int` de manera que la estructura(firma de la funcion) se vea así

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

En contraste, en muchos otros lenguajes como Java, el `if` es una **instrucción**, lo que significa que no tiene un valor y no puede ser usado directamente para asignaciones o en otros cálculos.
### Cuerpos de Expresiones
En kotlin se pueden simplificar funciones y no ponerle un cuerpo encerrado entre llaves, para lograr esto la funcion debera de ser de una **expresión**

La siguiente funcion esta en la forma **"cuerpo de bloque"** por que posee `{}`
```kotlin
fun max(a: Int,b: Int): Int{
  return if(a > b) a else b
}
```
si se observa `if(a > b) a else b` es una **expresión** por ende se puede llevar a la forma **"cuerpo de expresión"** eliminando `{}` y asignando el valor de la expreción a la función con un `=` quedando de la siguiente forma.
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
Kotlin tiene un sistema para generar getter y setter automaticos de los miembros de la clase

| Declaración                  | Getter     | Setter      | Visibilidad por defecto |
|-----------------------------|------------|-------------|-------------------------|
| `val propertyName: Type`    | Sí (Público) | No          | Pública                 |
| `var propertyName: Type`    | Sí (Público) | Sí (Público) | Pública                 |

Esta tabla resume cómo se generan los getters y setters en Kotlin:

- Cuando declaras una propiedad con `val`, se genera un getter público automáticamente, lo que permite acceder al valor de la propiedad desde cualquier lugar. No se genera un setter, ya que la propiedad es de solo lectura.

- Cuando declaras una propiedad con `var`, se generan tanto un getter público como un setter público automáticamente. Esto permite tanto leer como escribir el valor de la propiedad desde cualquier lugar.

Pero claro no estamos aplicando **buenas practicas** por ende debemos intancias los miembros de la clase con `private` esto afecta a la creacion de getter y setters por ende tocaria crearlos similar a java.
```kotlin
class Perso(private val name: String){
  fun getName() = this.name
  fun setName(newName:String){
    this.name = newName
  }
}
```
### Personalización de acesorios
En algunos casos es posible que no se necesite añadir un `private` a un miebro de una clase y los getters y setters se usen con normalidad, se pueden customizar o sobre escribir la logica
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
La clase `Rectangle` se tiene el atributo `isSquare` con un valor Boolean, pero ¿comó se define su valor?. En este caso el metodo `get() = height == width` define esa logica para el getter del atributo `isSquare`

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
Se basaron en el sistema `Switch case` para idear la estructura `when` esta permite el manejo de `enum class` de manera mas versatil y concisa, podemos decir que es tambien una **expresón** pues trabaja similar a un `if` por eso se pueden hacer cosas como
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
le pasamos a `getMnemonic` un objeto `Color` para que evalue su `enumValue` que puede ser `RED,ORANGE,YELLOW,GREEN,BLUE,INDIGO,VIOLET` dependiendo su `enumValue` determina el valor que retornara en el caso `getMnemonic(color.BLUE)` retornara `Battle`
