# KOTLIN IN ACTION - Cap 5

## Indice

1. [Introducción a las lambdas](#introducción-a-las-lambdas)
2. [Lambdas & colecciones](#lambdas--colecciones)
3. [Lambdas con receptores](#lambdas-con-receptores)
4. [Interfaces funcionales](#interfaces-funcionales)



## Introducción a las lambdas
Las lambdas son bloques de código cortos que se pueden pasar como argumentos a otras funciones, lo que evita la necesidad de definir funciones adicionales.

```kotlin
val suma: (Int, Int) -> Int = { a, b -> a + b }

fun main() {
    val resultado = suma(5, 3)
    println("El resultado de la suma es: $resultado")
}
```
En este ejemplo, suma es una variable que contiene una lambda que toma dos parámetros a y b de tipo Int y devuelve su suma. En la función main(), se utiliza esta lambda para sumar 5 y 3, y luego se imprime el resultado.

La lambda { a, b -> a + b } representa una función anónima que toma dos parámetros `"(a y b)"` y devuelve la suma de los mismos. En este caso, la expresión a + b calcula la suma de los dos números.

![Static Badge](https://img.shields.io/badge/sintaxis%20-%23FA8E5F?style=for-the-badge)

En Kotlin, las lambdas tienen una sintaxis clara y concisa, lo que las hace fáciles de usar y entender, mejorando la legibilidad del código. Su sintaxis se basa en:

El cuerpo de la lambda es una expresión o bloque de código ejecutado cuando se llama. Por ejemplo, una lambda que toma un argumento y devuelve el doble del valor del argumento:

```kotlin
val double = { x: Int -> x * 2 }
```
En este caso, x: Int es la lista de argumentos de la lambda y x * 2 es su cuerpo. La lambda toma un número entero x y devuelve el doble de ese número.

Se puede usar la sintaxis de referencia de función para crear una lambda.Por ejemplo:

```kotlin
val square: (Int) -> Int = Int::times
```
En este ejemplo, square es una función lambda que calcula el cuadrado de un número utilizando `Int::times` como la referencia al método times de la clase Int.

![Static Badge](https://img.shields.io/badge/Variables_capturadas_dentro_de_una_lambda%20-%23FACA89?style=for-the-badge)

En Kotlin, las lambdas pueden capturar variables del contexto en el que se definen, accediendo a variables locales y parámetros de la función contenedora.

>[!NOTE]
>Si la variable es inmutable, la lambda puede acceder a su valor en cualquier momento; si es mutable, solo puede acceder al valor actual en el momento de su llamada, manteniendo una referencia al valor anterior si cambia después de la creación de la lambda.

Para capturar una variable mutable en una lambda, puedes usar una clase de envoltura que almacene una referencia a la variable. Por ejemplo:

```kotlin
class Ref<T>(var value: T)

val counter = Ref(0)
val inc = { counter.value++ }
```
En este caso, la clase Ref es una envoltura que almacena una referencia a una variable mutable. La variable counter es una instancia de esta clase que almacena un valor entero. La variable inc es una lambda que captura counter y aumenta su valor en uno cada vez que se llama.

>[!IMPORTANT]
>Aunque la variable capturada es mutable, la referencia en la lambda es inmutable. Esto implica que la lambda no puede cambiar la referencia de la variable, pero sí puede cambiar su valor mediante la referencia almacenada.


#### _~Clase de envoltura~_
Una clase de envoltura almacena una referencia a un valor, pudiendo ser mutable o inmutable. En el caso de ser mutable, el valor puede cambiar; en el caso de ser inmutable, no puede cambiar. Por ejemplo, la clase genérica 'Ref<T>' almacena un valor de cualquier tipo 'T' con una propiedad llamada '"value"' para acceder y modificar ese valor.

### Lambdas & colecciones
En Kotlin, las lambdas se usan para definir funciones que pueden ser pasadas como argumentos a funciones de extensión de colecciones. Por ejemplo, Kotlin ofrece  funciones de extensión como map, reduce, fold, forEach, groupBy, sortedBy, entre otras, que permiten operar sobre colecciones de datos de forma concisa y legible.

- `filter:` Devuelve una nueva colección con elementos que cumplen una condición.
- `map:` Devuelve una nueva colección con los resultados de aplicar una función a cada elemento.
- `reduce/fold:` Combina elementos en un valor único usando una función.
- `forEach:` Ejecuta una acción en cada elemento de la colección.
- `groupBy:` Agrupa elementos en subcolecciones según una clave.
- `sortedBy:` Devuelve una nueva colección ordenada según una clave.

Estas funciones son comúnmente usadas para operar sobre colecciones de datos.Además, Kotlin ofrece otras funciones de extensión para manipular colecciones, como `zip`, `flatten`, `distinct`, `partition`, y más.


### Lambdas con receptores

permiten llamar métodos de un objeto dentro del cuerpo de la lambda sin necesidad de calificarlos adicionalmente, funcionando como métodos de ese objeto específico. 

>[!NOTE]
>Esto una característica única de Kotlin.

La sintaxis para definir una lambda con receptor es la siguiente:
```kotlin
val lambda: ReceiverType.() -> ReturnType = { /* lambda body */ }
```

En esta sintaxis, 'ReceiverType' es el tipo de objeto usado como receptor en la lambda, y 'ReturnType' es el tipo de valor que devuelve. La lambda se define entre llaves y puede llamar a métodos del receptor sin calificarlos.


por ejemplo:

```kotlin
class Person {
    var name: String = ""
    var age: Int = 0
}

fun person(block: Person.() -> Unit): Person = Person().apply(block)

val person = person {
    name = "Alice"
    age = 30
}
```
Esta es una implementación de una función 'person' que toma una lambda con receptor para configurar una instancia de la clase 'Person'. Dentro de la lambda, los métodos 'name' y 'age' de la instancia de Person se pueden llamar directamente.

>[IMPORTANT]
> Las lambdas con receptores son una característica poderosa de Kotlin que se utilizan a menudo para crear DSL (Domain-Specific Languages) y para simplificar la configuración de objetos complejos.

### Interfaces funcionales
En Java y Kotlin, una interfaz funcional tiene exactamente un método abstracto y se usa para representar funciones o acciones que se pueden pasar como argumentos a métodos o lambdas.

Algunos ejemplos incluyen:

- `Runnable:` Interfaz para acciones sin argumentos ni retorno.
- `Callable:` Interfaz para acciones con argumentos y retorno.
- `Comparator:` Interfaz para comparar objetos y determinar su orden relativo.

```kotlin
val runnable = Runnable { println("Hello, world!") }
Thread(runnable).start()
```
Se instancia una interfaz `Runnable` con una lambda que imprime "Hello, world!", y luego se crea un nuevo hilo de ejecución con esta instancia.