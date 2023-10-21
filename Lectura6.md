# 1. Introducción a los Activitys
En Android, las actividades son componentes clave de una aplicación y se utilizan para gestionar la interacción del usuario con la aplicación. Cada actividad representa una pantalla o una parte de la interfaz de usuario de la aplicación. A continuación, se presenta un resumen de los conceptos clave relacionados con las actividades en Android, junto con ejemplos de código en lenguaje Kotlin:
## Indice
- [1. Introducción a los Activitys](#1-introducción-a-los-activitys)
  - [Indice](#indice)
  - [1. Concepto de Actividades:](#1-concepto-de-actividades)
  - [2. Configuración del Manifiesto:](#2-configuración-del-manifiesto)
  - [3. Filtros de Intents:](#3-filtros-de-intents)
  - [4. Permisos:](#4-permisos)
  - [5. Ciclo de Vida de la Actividad:](#5-ciclo-de-vida-de-la-actividad)
- [2. Ciclo de vida de una Actividad](#2-ciclo-de-vida-de-una-actividad)
  - [1. `onCreate()`:](#1-oncreate)
  - [2. `onStart()`](#2-onstart)
  - [3. `onResume()`](#3-onresume)
  - [4. `onPause()`](#4-onpause)
  - [5. `onStop()`](#5-onstop)
  - [6. `onDestroy()`](#6-ondestroy)
  - [7. Guardar y Restaurar el Estado de la IU](#7-guardar-y-restaurar-el-estado-de-la-iu)
  - [8. Iniciar Actividades](#8-iniciar-actividades)
  - [9. Coordinación de Actividades](#9-coordinación-de-actividades)
- [3. Guía de Android: Manejo de Cambios de Estado en Actividades](#3-guía-de-android-manejo-de-cambios-de-estado-en-actividades)
    - [Caso 1: Cambio de Configuración](#caso-1-cambio-de-configuración)
    - [Caso 2: Modo Multiventana](#caso-2-modo-multiventana)
    - [Caso 3: Actividad o Diálogo en Primer Plano](#caso-3-actividad-o-diálogo-en-primer-plano)
    - [Caso 4: El Usuario Toca el Botón "Atrás"](#caso-4-el-usuario-toca-el-botón-atrás)
    - [Caso 5: El Sistema Elimina el Proceso de la App](#caso-5-el-sistema-elimina-el-proceso-de-la-app)

## 1. Concepto de Actividades:
Las actividades son una parte fundamental del modelo de aplicación de Android. Cada actividad representa una pantalla o una parte de la interfaz de usuario de la aplicación.

Ejemplo: Una actividad de una aplicación de correo electrónico podría representar la bandeja de entrada, mientras que otra actividad podría representar la pantalla de redacción de un correo.

   - Las actividades son una parte fundamental del modelo de aplicación de Android.
   - Cada actividad representa una pantalla o una parte de la interfaz de usuario de la aplicación.
   - Ejemplo: Una actividad de una aplicación de correo electrónico podría representar la bandeja de entrada, mientras que otra actividad podría representar la pantalla de redacción de un correo.

## 2. Configuración del Manifiesto:
   - Para que la aplicación utilice actividades, debes declararlas en el archivo de manifiesto de la aplicación.
   - Ejemplo de declaración de actividad en el manifiesto:
   ```kotlin
   <activity android:name=".ExampleActivity" />
   ```

## 3. Filtros de Intents:
   - Los filtros de intents permiten que las actividades respondan a solicitudes explícitas o implícitas.
   - Ejemplo de configuración de un filtro de intent en una actividad:
   ```kotlin
   <intent-filter>
       <action android:name="android.intent.action.SEND" />
       <category android:name="android.intent.category.DEFAULT" />
       <data android:mimeType="text/plain" />
   </intent-filter>
   ```

## 4. Permisos:
   - Puedes controlar qué aplicaciones pueden iniciar una actividad mediante la declaración de permisos en el manifiesto.
   - Ejemplo de declaración de permisos en el manifiesto:
   ```kotlin
   <uses-permission android:name="com.google.socialapp.permission.SHARE_POST" />
   ```


# 2. Ciclo de vida de una Actividad

El ciclo de vida de una actividad es una parte fundamental del modelo de aplicación de Android. Cada actividad pasa por varios estados a lo largo de su vida útil, y estos estados se gestionan mediante devoluciones de llamada.

## 1. `onCreate()`: 

Este método se llama cuando el sistema crea la actividad por primera vez. Aquí, debes realizar la inicialización básica, como configurar la interfaz de usuario y vincular datos. También puedes recuperar el estado previamente guardado de la actividad a través del parámetro `savedInstanceState`. Es una buena práctica realizar cualquier trabajo que deba ocurrir solo una vez en la vida de la actividad en este método.
```kotlin
override fun onCreate(savedInstanceState: Bundle?) {
    super.onCreate(savedInstanceState)
    setContentView(R.layout.activity_main)
}
```
En el código anterior, el método `onCreate()` se llama cuando se crea la actividad. Aquí, se llama al método `setContentView()` para establecer el diseño de la actividad en la pantalla. También se puede recuperar el estado previamente guardado de la actividad a través del parámetro `savedInstanceState`.

## 2. `onStart()`
 Se llama cuando la actividad entra en el estado "Started", lo que significa que la app se está preparando para interactuar con el usuario. En este punto, puedes iniciar cualquier código relacionado con la interfaz de usuario.

```kotlin
override fun onStart() {
    super.onStart()
    // Inicia cualquier código relacionado con la interfaz de usuario
}
```
En el código anterior, el método `onStart()` se llama cuando la actividad entra en el estado "Started". Aquí, puedes iniciar cualquier código relacionado con la interfaz de usuario.

## 3. `onResume()`
 Cuando la actividad entra en el estado "Resumed", significa que se encuentra en primer plano y es visible para el usuario. Aquí, debes habilitar cualquier funcionalidad que requiera interacción del usuario. Si tienes componentes que priorizan el ciclo de vida, este es un buen lugar para activarlos.
 ```kotlin
    override fun onResume() {
        super.onResume()
        // Habilita cualquier funcionalidad que requiera interacción del usuario
    }
```
En el código anterior, el método `onResume()` se llama cuando la actividad entra en el estado "Resumed". Aquí, puedes habilitar cualquier funcionalidad que requiera interacción del usuario.

## 4. `onPause()`
 Este método se llama cuando la actividad está a punto de perder el foco o ser parcialmente visible (por ejemplo, en el modo multiventana). Debes pausar o ajustar cualquier operación que no deba continuar mientras la actividad esté en este estado. También puedes liberar recursos no necesarios para ahorrar energía y recursos del sistema. Es importante recordar que la actividad no necesariamente pasará inmediatamente al siguiente estado después de `onPause()`.
```kotlin
    override fun onPause() {
        super.onPause()
        // Pausa o ajusta cualquier operación que no deba continuar mientras la actividad esté en este estado
    }
```

## 5. `onStop()`
 Cuando la actividad ya no es visible para el usuario (por ejemplo, cuando se lanza otra actividad que cubre la pantalla o el usuario navega a otra aplicación), se llama a `onStop()`. En este punto, debes liberar recursos y detener cualquier operación relacionada con la interfaz de usuario que no sea necesaria mientras la actividad está en segundo plano. Es importante para ahorrar recursos y mejorar la experiencia del usuario en el modo multiventana.
```kotlin
    override fun onStop() {
        super.onStop()
        // Libera recursos y detiene cualquier operación relacionada con la interfaz de usuario que no sea necesaria mientras la actividad está en segundo plano
    }
```
## 6. `onDestroy()`
 Esta devolución de llamada se llama antes de que la actividad se destruya por completo. Puedes usarla para liberar cualquier recurso que todavía esté en uso y que no se liberó en los métodos anteriores. También es donde puedes realizar operaciones finales antes de que la actividad se cierre por completo.

```kotlin
    override fun onDestroy() {
        super.onDestroy()
        // Libera cualquier recurso que todavía esté en uso y que no se liberó en los métodos anteriores
    }
```

La relación entre los estados del ciclo de vida de una actividad es importante para comprender cómo funcionan las actividades en Android. Es importante recordar que el sistema puede llamar a los métodos `onPause()` y `onStop()` en cualquier momento, entonces debes asegurarte de que tu aplicación esté preparada para manejar estos cambios de estado.


## 7. Guardar y Restaurar el Estado de la IU
 Cuando una actividad se encuentra en el estado "Paused" o "Stopped", puede ser finalizada por el sistema en caso de que se necesite liberar memoria. En tales casos, es importante guardar el estado transitorio de la IU de la actividad, como el contenido de campos de texto, en un objeto `Bundle` en el método `onSaveInstanceState()`. Cuando se recrea la actividad, puedes recuperar este estado del `Bundle` en los métodos `onCreate()` o `onRestoreInstanceState()`, permitiendo que la IU vuelva a su estado anterior.

## 8. Iniciar Actividades
 Puedes iniciar una nueva actividad en tu aplicación utilizando el método `startActivity()` si no esperas un resultado de la nueva actividad. Si deseas obtener un resultado de la actividad que se inicia, puedes usar `startActivityForResult()`. Esto es útil cuando, por ejemplo, deseas abrir una actividad para seleccionar un contacto y obtener el contacto seleccionado como resultado.

## 9. Coordinación de Actividades
 Cuando una actividad inicia otra, ambas pueden estar en diferentes estados de su ciclo de vida. La actividad actual entra en el estado "Paused" o "Stopped" mientras se crea la nueva actividad. Es importante entender el orden en que se ejecutan las devoluciones de llamada del ciclo de vida para coordinar la transición de datos y asegurarse de que la información se conserve correctamente.

# 3. Cómo administrar los cambios de estado de la actividad en Android

Diferentes eventos, activados por el usuario y el sistema, pueden provocar cambios en el estado de una `Activity` en Android. Aquí, describiremos algunos casos comunes en los que ocurren estas transiciones y cómo administrarlas.

Supongamos que estás desarrollando una aplicación en Android y deseas garantizar que tu actividad se comporte de manera adecuada al cambiar la orientación del dispositivo o al cambiar el idioma.

## Caso 1: Cambio de Configuración

Un cambio de configuración, como la rotación del dispositivo o el cambio de idioma, puede llevar a que la actividad se destruya y vuelva a crearse. La instancia original de la actividad pasa por los métodos `onPause()`, `onStop()` y `onDestroy()`, mientras que una nueva instancia se crea y activa mediante `onCreate()`, `onStart()`, y `onResume()`.

```kotlin
class MiActividad : AppCompatActivity() {
    // ...
    override fun onConfigurationChanged(newConfig: Configuration) {
        super.onConfigurationChanged(newConfig)
        // Handle configuration changes
    }
}
```
En el código anterior, el método `onConfigurationChanged()` se llama cuando se produce un cambio de configuración. Aquí, puedes administrar el cambio de configuración.

## Caso 2: Modo Multiventana

Cuando una aplicación entra en modo multiventana en Android 7.0 y versiones posteriores, se notifica a la actividad en ejecución sobre un cambio de configuración. La actividad puede administrar este cambio o permitir que el sistema elimine la actividad y la vuelva a crear con las nuevas dimensiones.

```kotlin
class MiActividad : AppCompatActivity() {
    // ...
    override fun onMultiWindowModeChanged(isInMultiWindowMode: Boolean, newConfig: Configuration) {
        super.onMultiWindowModeChanged(isInMultiWindowMode, newConfig)
        // Handle multi-window mode changes
    }
}
```
En el código anterior, el método `onMultiWindowModeChanged()` se llama cuando se produce un cambio en el modo multiventana. Aquí, puedes administrar el cambio de modo multiventana.

### Caso 3: Actividad o Diálogo en Primer Plano

Si una nueva actividad o diálogo aparece en primer plano y cubre parcial o completamente la actividad en progreso, la actividad en segundo plano puede pasar al estado `Detenida`. Cuando la actividad cubierta vuelve al primer plano, se activa `onResume()`. Puede personalizarse el comportamiento del botón "Atrás".

```kotlin
class MiActividad : AppCompatActivity() {
    // ...
    override fun onPause() {
        super.onPause()
        // Handle when the activity goes into the background
    }
}
```
En el código anterior, el método `onPause()` se llama cuando la actividad entra en el estado "Paused". Aquí, puedes administrar el comportamiento cuando la actividad pasa al segundo plano.
### Caso 4: El Usuario Toca el Botón "Atrás"

Cuando el usuario toca el botón "Atrás" y una actividad está en primer plano, la actividad pasa por `onPause()`, `onStop()` y `onDestroy()`. Además, la actividad se quita de la pila de actividades. Por defecto, `onSaveInstanceState()` no se activa en este caso, pero se puede personalizar.

```kotlin
class MiActividad : AppCompatActivity() {
    // ...
    override fun onBackPressed() {
        super.onBackPressed()
        // Handle the custom behavior for the "Back" button
    }
}
```
En el código anterior, el método `onBackPressed()` se llama cuando el usuario toca el botón "Atrás". Aquí, puedes administrar el comportamiento personalizado para el botón "Atrás".
### Caso 5: El Sistema Elimina el Proceso de la App

Si una aplicación está en segundo plano y el sistema necesita liberar memoria, puede eliminar el proceso en segundo plano para liberar más recursos.





