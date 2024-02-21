# KOTLIN IN ACTION - Cap 3

## Indice

1. [Collections](#Collections)
2. [Parámetros de funciones](#parámetros-de-funciones)
3. [Funciones de nivel superior](#funciones-de-nivel-superior)
4. [Funciones de extensión](#funciones-de-extensión)
5. [Override](#override)
6. [Varargs, Infix calls & Destructuring](#varargs-infix-calls--destructuring)
7. [Funciones locales y extensiones](#funciones-locales-y-extensiones)

## Collections
En Kotlin, aunque la sintaxis para crear una clase Collection difiere de Java, en esencia, Kotlin utiliza la implementación de Collection de Java. La diferencia radica en que Kotlin emplea una sintaxis más concisa para su creación.

```kotlin
  val set = hashSetOf(1, 7, 53)
  val list = arrayListOf(1, 7, 53)
  val map = hashMapOf(1 to "one", 7 to "seven", 53 to "fifty-three")
```

En ciertos escenarios, es necesario modificar colecciones para diversas situaciones, como exportar datos a un archivo o realizar análisis de datos. Para ello, se puede utilizar funciones como joinToString(), que convierte una colección en una cadena de texto. Veamos un ejemplo de esto:

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

## Parámetros de funciones

- `collection:` La colección a convertir en cadena de texto.
- `separator:` El separador entre los elementos de la colección.
- `prefix:` El prefijo al inicio de la cadena.
- `postfix:` El sufijo al final de la cadena.

para esto kotlin recomienda seguir buenas prácticas, como usar comentarios o nombres de parámetros en las funciones, con el fin de proporcionar contexto al enviar parámetros a una función y evitar confusiones futuras.

```kotlin
list.joinToString(/*separador*/"; ", /*prefijo */"(", /*sufijo*/")")
```

Por ejemplo:

```kotlin
  val list = listOf(1, 2, 3)
  println(list.joinToString(separator = "; ", prefix = "(", postfix = ")"))
```
`Resultado: (1; 2; 3)`

### _Valores por defecto_
En Kotlin, se pueden establecer valores por defecto para los parámetros de una función, lo que significa que no es obligatorio proporcionar todos los parámetros al llamar la función, sino solo aquellos que se requieran. Por ejemplo, en la función joinToString() se pueden definir valores por defecto para sus parámetros, lo que simplifica su uso al permitir enviar solo los parámetros necesarios al llamarla.

```kotlin
fun <T> joinToString(
    collection: Collection<T>,
    separator: String = ", ",
    prefix: String = "",
    postfix: String = ""
): String {}
```
```kotlin
val list = listOf(1, 2, 3)
println(list.joinToString())
```

## Funciones de nivel superior
En Kotlin, las funciones de nivel superior pueden estar fuera de una clase, al mismo nivel que las clases, como la función `suma()` y `main()` que veremos en el siguiente ejemplo. 
 
```kotlin
public final class MainKt {
   public static final int suma(int a, int b) {
      return a + b;
   }

   public static final void main() {
      int resultado = sumar(5, 3);
      String var2 = "El resultado de la suma es: " + resultado;
      System.out.println(var2);
   }
}
```

A diferencia de Java, no es necesario encapsularlas dentro de clases. Internamente, Kotlin convierte estas funciones en métodos estáticos de una clase, lo que garantiza la compatibilidad con Java.

> [!IMPORTANT]
> En Kotlin, tambien puedes declarar variables de nivel superior que son accesibles en todo el código, no limitadas a una clase.

```kotlin
val PI = 3.1416
val nombre = "Juan"
```

## Funciones de extensión
En Kotlin, se pueden agregar funciones a una clase sin la necesidad de modificar la clase, utilizando funciones de extensión. Por ejemplo, si queremos agregar una función a la clase `Animal` para determinar si es un animal adulto, podemos hacerlo mediante una función de extensión.

```kotlin
Class Animal{
  var especie:String
  var edad:Int
}
```
 
Sin embargo, estas funciones tienen limitaciones, como no poder acceder a atributos privados de la clase, lo que ayuda a mantener el principio de encapsulamiento. Además, las funciones de extensión solo pueden ser utilizadas en el archivo donde se declaran o en archivos específicos.

### Importaciones en funciones de extensión
Para importar una función de extensión, se utiliza la palabra clave `"import"` seguida del nombre del archivo que contiene la función. Se puede importar todas las funciones de extensión de un archivo usando `"*"` o cambiar el nombre de la función al importarla usando `"as"`.

```kotlin
import NombreDelArchivo.funcionDeExtension

import NombreDelArchivo.*

import NombreDelArchivo.funcionDeExtension as nombreDeLaFuncion
```

## Override
En Kotlin, puedes sobrescribir funciones de una clase padre en una clase hija usando la palabra clave `override`. Por ejemplo:

```kotlin
open class View {
    open fun click() = println("View clicked")
}

class Button : View() {
    override fun click() = println("Button clicked")
}

fun main() {
    val view: View = Button()
    view.click()
}
```
Al crear un objeto del tipo `Button` y llamar a la función `click()`, se ejecutará la implementación de la clase `Button` en lugar de la de la clase `View`.

>[!NOTA]
> Si una clase posee una función miembro con la misma firma que una función de extensión, la función miembro prevalecerá en todo momento.


## Varargs, Infix calls & Destructuring

Kotlin introduce la palabra clave `vararg`, permitiendo funciones que reciben un número variable de argumentos del mismo tipo, simplificando el paso de múltiples valores a una función sin necesidad de empaquetarlos previamente. Por ejemplo:
```kotlin
fun printNumbers(vararg numbers: Int) {
    for (number in numbers) {
        println(number)
    }
}

printNumbers(1, 2, 3) // Imprime: 1 2 3
```
>[!NOTE]
> Con un `*` se puede desempaquetar listas o arrays para mandarlos como argumentos de una función.

```kotlin
val list = listOf(1, 2, 3)
printNumbers(*list.toIntArray()) // Imprime: 1 2 3
```

la notación `infix` te permite utilizar funciones de un solo argumento de manera más concisa, sin necesidad de usar puntos ni paréntesis al llamarlas. Por ejemplo:

```kotlin
infix fun Int.times(str: String) = str.repeat(this)

println(3 times "Plantita ") // Imprime: Plantita Plantita Plantita
```


La `desestructuración` permite desempaquetar elementos de una estructura de datos en múltiples variables. Por ejemplo:

```kotlin
val (name, age) = person // Suponiendo que person es un objeto con propiedades name y age
println("$name tiene $age años")
```


## Funciones locales y extensiones
En Kotlin, es posible crear funciones dentro de otras funciones con el fin de eliminar la repetición de código.

Por ejemplo, el siguiente código es algo repetitivo:

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

Para evitar esto, se puede introducir una función dentro de la función `saveUser()` que se encargue de validar los campos de la clase `"User"`.

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