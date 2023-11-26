## Resumen de la Documentación de Android: Menús

### Introducción

La documentación de Android sobre menús proporciona información detallada sobre la creación y gestión de menús en aplicaciones Android. Los menús son elementos cruciales para la interfaz de usuario, permitiendo a los usuarios acceder a diversas funciones de la aplicación de manera intuitiva.

### Índice

1. **[Tipos de Menús](#tipos-de-menús)**
2. **[Creación de Menús](#creación-de-menús)**
3. **[Definición en XML](#definición-en-xml)**
4. **[Manejo de Eventos](#manejo-de-eventos)**
5. **[Menús Contextuales](#menús-contextuales)**
6. **[Ejemplos de Código](#ejemplos-de-código)**

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

```java
@Override
public boolean onCreateOptionsMenu(Menu menu) {
    getMenuInflater().inflate(R.menu.options_menu, menu);
    return true;
}

@Override
public boolean onOptionsItemSelected(MenuItem item) {
    switch (item.getItemId()) {
        case R.id.menu_item:
            // Acción asociada al elemento del menú
            return true;
        default:
            return super.onOptionsItemSelected(item);
    }
}
```

#### Menús Contextuales:

```java
@Override
public void onCreateContextMenu(ContextMenu menu, View v, ContextMenu.ContextMenuInfo menuInfo) {
    super.onCreateContextMenu(menu, v, menuInfo);
    getMenuInflater().inflate(R.menu.context_menu, menu);
}

@Override
public boolean onContextItemSelected(MenuItem item) {
    switch (item.getItemId()) {
        case R.id.context_menu_item:
            // Acción asociada al elemento del menú contextual
            return true;
        default:
            return super.onContextItemSelected(item);
    }
}
```

Este resumen proporciona una visión general de la documentación de Android sobre menús, cubriendo la creación, tipos y manejo de eventos. Para detalles completos, se recomienda revisar la documentación oficial.