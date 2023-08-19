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


