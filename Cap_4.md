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

