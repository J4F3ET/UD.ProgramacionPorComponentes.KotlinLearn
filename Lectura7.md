# ¿Qué son layouts?
## Indice
- [Introducción](#introducción)
- [Existen dos formas de declarar un diseño en Android](##existen-dos-formas-de-declarar-un-diseño-en-Android)
- [Estructura básica de un diseño XML](##estructura-básica-de-un-diseño-XML)
- [Atributos de diseño](##atributos-de-diseño)
## Introducción
En Android, un diseño es una estructura que define la disposición de los elementos de la interfaz de usuario (UI) de una aplicación. Los diseños se utilizan para organizar los elementos de la UI de una manera lógica y eficiente.

## Existen dos formas de declarar un diseño en Android:

- **Declarar elementos de la UI en XML**. Android proporciona un vocabulario XML simple que coincide con las clases y subclases de vistas, como las que se usan para widgets y diseños.
- **Usar el editor de diseño de Android Studio**. El editor de diseño proporciona una interfaz gráfica de usuario (GUI) que le permite crear diseños arrastrando y soltando elementos de la UI.
Declarar un diseño en XML

Para declarar un diseño en XML, debe crear un archivo XML con la extensión .xml. El archivo XML debe contener una etiqueta raíz que defina el tipo de diseño que desea crear.

## Estructura básica de un diseño XML

La estructura básica de un diseño XML es la siguiente:
```xml
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android">
    <TextView
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Hello, world!" />
</RelativeLayout>

```
En este ejemplo, el diseño tiene una sola vista, un TextView. El TextView tiene un ancho y una altura que se ajustan al ancho y la altura del padre. El texto del TextView es "Hello, world!".

## Atributos de diseño

Los diseños pueden tener una variedad de atributos que controlan su apariencia y comportamiento. Algunos atributos de diseño comunes incluyen:

- `layout_width`: El ancho del diseño.
- `layout_height`: La altura del diseño.
- `layout_margin`: Los márgenes del diseño.
- `layout_padding`: Los rellenos del diseño.
- `layout_gravity`: La gravedad del diseño.
### Ejemplo de diseño XML
El siguiente ejemplo muestra un diseño que contiene dos TextView. El primer TextView tiene un ancho y una altura que se ajustan al ancho y la altura del padre. El segundo TextView tiene un ancho de 100 píxeles y una altura de 20 píxeles. Los dos TextView están alineados horizontalmente en el centro del diseño.
```xml
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android">
    <TextView
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Texto 1" />
    <TextView
        android:layout_width="100dp"
        android:layout_height="20dp"
        android:text="Texto 2" />
</RelativeLayout>
```
