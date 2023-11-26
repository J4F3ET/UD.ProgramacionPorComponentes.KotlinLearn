## Resumen de la Documentación de Android: Menús

### Introducción

La documentación de Android sobre menús proporciona información detallada sobre la creación y gestión de menús en aplicaciones Android. Los menús son elementos cruciales para la interfaz de usuario, permitiendo a los usuarios acceder a diversas funciones de la aplicación de manera intuitiva.

### Índice

- [Tipos de Menús](#tipos-de-menús)
- [Creación de Menús](#creación-de-menús)
- [Definición en XML](#definición-en-xml)
- [Manejo de Eventos](#manejo-de-eventos)
- [Menús Contextuales](#menús-contextuales)
- [Ejemplos de Código](#ejemplos-de-código)

### Tipos de Menús

Existen dos tipos principales de menús en Android:

- **Opciones del menú de la aplicación:** Están ubicadas en la barra de aplicaciones y proporcionan opciones específicas de la aplicación.
- **Menús contextuales:** Se muestran en respuesta a una acción prolongada y contienen acciones contextuales relacionadas con el elemento seleccionado.

### Creación de Menús

Los menús en Android se pueden crear de dos maneras:

- **Programáticamente:** Creando instancias de objetos `Menu` y agregando elementos mediante métodos.
- **Declarativamente:** Definiendo menús en archivos XML y luego inflándolos en el código.

### Definición en XML

La definición de menús en XML facilita la gestión y la modularidad. Un ejemplo básico de un menú de opciones en XML:

```xml
<menu xmlns:android="http://schemas.android.com/apk/res/android">
    <item
        android:id="@+id/menu_item"
        android:title="Opción del Menú"
        android:icon="@drawable/ic_menu_icon"/>
</menu>
```

### Manejo de Eventos

El manejo de eventos en menús se realiza a través de métodos como `onCreateOptionsMenu` y `onOptionsItemSelected`. Estos métodos permiten la creación y gestión de acciones asociadas a elementos de menú.

### Menús Contextuales

Los menús contextuales son útiles para acciones específicas sobre un elemento. Para implementarlos, se utiliza el método `onCreateContextMenu` junto con `onContextItemSelected`.

### Ejemplos de Código

#### Creación Programática de Menús:

```kotlin
// Menú de opciones
override fun onCreateOptionsMenu(menu: Menu): Boolean {
    menuInflater.inflate(R.menu.options_menu, menu)
    return true
}

override fun onOptionsItemSelected(item: MenuItem): Boolean {
    when (item.itemId) {
        R.id.menu_item -> {
            // Acción asociada al elemento del menú
            return true
        }
        else -> return super.onOptionsItemSelected(item)
    }
}
```
En el ejemplo anterior, `R.menu.options_menu` es el archivo XML que contiene la definición del menú de opciones. El método `onCreateOptionsMenu` infla el menú y lo muestra en la barra de aplicaciones. El método `onOptionsItemSelected` maneja los eventos de los elementos del menú.

#### Menús Contextuales:

```kotlin
// Menú contextual
override fun onCreateContextMenu(menu: ContextMenu, v: View, menuInfo: ContextMenu.ContextMenuInfo) {
    super.onCreateContextMenu(menu, v, menuInfo)
    menuInflater.inflate(R.menu.context_menu, menu)
}

override fun onContextItemSelected(item: MenuItem): Boolean {
    when (item.itemId) {
        R.id.context_menu_item -> {
            // Acción asociada al elemento del menú contextual
            return true
        }
        else -> return super.onContextItemSelected(item)
    }
}
```
En el ejemplo anterior, `R.menu.context_menu` es el archivo XML que contiene la definición del menú contextual. Además, `v` es la vista que se ha mantenido presionada para mostrar el menú contextual. Por último, `menuInfo` contiene información sobre el elemento seleccionado.