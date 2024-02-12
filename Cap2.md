# KOTLIN IN ACTION - Cap 2

## Indice

1. [Variables](#variables)
2. [Funciones](#funciones)
3. [Expresiones & Instrucciones](#expresiones--instrucciones)
4. [Clases & Propiedades](#clases--propiedades)
5. [Estrucutura when & Bucles](#estrucutura-when--bucles)
6. [Cast en kotlin](#cast-en-kotlin)
7. [Rangos](#rangos)
8. [Excepciones](#excepciones-try-catch)
9. [Exportaciones e importaciones](#exportaciones-e-importaciones)


## Variables
Primeramente se debe saber que Kotlin nos propone implementar datos inmutables, en lugar de mutables. 

- `val` (de valor): Es una referencia inmutable. Una vez inicializada, una variable declarada con "val" no puede ser reasignada.

- `var` (de variable): Es una referencia mutable. El valor de una variable de este tipo puede ser cambiado después de su inicialización.

Como se mencionó anteriormente, en Kotlin se declara una variable comenzando con una palabra clave, y opcionalmente se puede especificar el tipo después del nombre de la variable.

``` kotlin
val answer = 4.2
val answer: Int = 42
```
## Funciones
Observemos la estructura basica de una funcion:

![Imagen](/Imagens/Estructura_funcion.png)


> [!NOTE]
> fun-> se utiliza para declarar una función

Observemos un ejemplo de esto:

``` kotlin
data class person(
    val name:String
    val age:Int? = null
)

fun main(args: Array<String>) {
    val persons = listOf(Person("Alice"),Person("Bob", age = 29))
    val oldest = persons.maxBy { it.age ?: 0 }
}
```
## Expresiones & Instrucciones
En Kotlin, comprender la diferencia entre expresiones e instrucciones es fundamental, ya que afecta el comportamiento de ciertas estructuras y su uso en diferentes contextos.

Las expresiones tienen valor y se usan donde se necesita un valor, como en (a + b). Las instrucciones, en cambio, realizan acciones sin generar un valor directo, como en (a = 10), que simplemente asigna un valor sin producir otro valor.

> [!IMPORTANT]
> En Kotlin, el `if` funciona como una expresión, lo que significa que tiene un valor y puede ser usado directamente en asignaciones o cálculos adicionales. Ejemplo: `val x = if (condición) 10 else 20`

Con Kotlin, puedes simplificar funciones usando Cuerpos de Expresiones, eliminando las llaves {}. La función debe ser una expresión para hacerlo.

La siguiente función está en forma de "cuerpo de bloque" debido a que posee llaves {}:
```kotlin
fun max(a: Int, b: Int): Int {
    return if (a > b) a else b
}
```
La expresión `if (a > b)` a else b se puede convertir a la forma de "cuerpo de expresión" eliminando las llaves {} y asignando el valor de la expresión a la función con un signo igual. También podemos omitir el tipo de dato que retorna.
```kotlin
fun max(a: Int, b: Int) = if (a > b) a else b
```

## Clases & Propiedades
Kotlin ofrece algunas propiedades en comparación con las clases en Java que resaltan su flexibilidad y concisión. Al comparar Kotlin con Java, podemos identificar algunas diferencias clave que demuestran las ventajas del primero en términos de claridad y eficiencia en el desarrollo de clases.

![Static Badge](https://img.shields.io/badge/~JAVA~%20-%2354C6B8?style=for-the-badge)
```java
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
![Static Badge](https://img.shields.io/badge/~KOTLIN~%20-%23C398C8?style=for-the-badge)
```kotlin
class Person(val name: String){}
```
En Kotlin, "public" es la visibilidad por defecto, a diferencia de Java. Por lo tanto, podemos omitirla al declarar clases, aunque también podemos declararla explícitamente si es necesario.
```kotlin
class Perso(private val name: String){}
```
Ahora entendamos que en Kotlin, se implementa un sistema para la generación automática de getter y setter para los miembros de la clase.

Al usar `val`, se crea un getter público para lectura de la propiedad. Con `var`, se generan tanto `getter` como `setter` públicos, permitiendo la lectura y escritura de valores cualquier parte del código.

La siguiente tabla resume cómo se generan los getters y setters en Kotlin:

| Declaración | Getter| Setter| Visibilidad por defecto |
|-----------------------------|------------|-------------|-------------------------|
| `val`    | Sí (Público) | No | Pública  |
| `var`    | Sí (Público) | Sí | Pública |

### _Data class_
Las data class en Kotlin son clases especializadas para representar datos de manera concisa. Se generan automáticamente métodos estándar como equals, hashCode y toString basados en las propiedades declaradas. 

Las data class en Kotlin ofrecen:

- Generación automática de métodos estándar como equals, hashCode y toString, basados en las propiedades.
- Desestructuración, permitiendo acceder a las propiedades de manera individual.
- Copiado simplificado a través del método copy() modificando propiedades específicas.
- Comparación de contenido para igualdad.
- Declaratividad en la definición de la estructura de datos.
- Beneficios en estructuras de datos como listas, conjuntos y mapas debido a su implementación automática de equals y hashCode.

Aquí tienes un ejemplo de cómo se declara y utiliza una data class:
```kotlin
data class Person(val name: String, val age: Int)

fun main() {
    val person1 = Person("Alice", 30)
    val person2 = Person("Bob", 25)

    println(person1) // Imprime: Person(name=Alice, age=30)
    println(person1 == person2) // Imprime: false

    val (name, age) = person1 // Desestructuración
    println("Name: $name, Age: $age")
}
```

### _Enum class_
Una enum class en Kotlin define un tipo de datos con un conjunto fijo de valores constantes, conocidos como "miembros de la enumeración". Por ejemplo:
```kotlin
enum class Color {
RED, ORANGE, YELLOW, GREEN, BLUE, INDIGO, VIOLET
}
```
Las enumeraciones en Kotlin representan instancias únicas de una clase, como RED, ORANGE, YELLOW, etc., cada una asociada con un color específico. Su uso evita errores tipográficos y ofrece un conjunto controlado de opciones. Además, permiten agregar propiedades y métodos para mejorar su funcionalidad. 

En resumen, las enum class en Kotlin proporcionan una forma segura y conveniente de definir tipos de datos con un conjunto limitado y conocido de valores posibles.


## Estrucutura when & Bucles
La estructura "when" en Kotlin es similar al "switch case" de Java pero más flexible, comparando diversos tipos de objetos como Int, String, Boolean, Enum class, entre otros. Funciona como una expresión, permitiendo un manejo conciso y versátil del código, similar a un "if".
```kotlin
fun getMnemonic(color: Color) =
    when (color) {
        Color.RED -> "Richard"
        Color.ORANGE -> "Of"
        Color.YELLOW -> "York"
        Color.GREEN -> "Gave"
        Color.BLUE -> "Battle"
        Color.VIOLET -> "Vain"
    }
println(getMnemonic(Color.BLUE))
>>> Battle
```
### _Manejo del when_
En Kotlin, 'when' permite agrupar valores para tomar decisiones. Por ejemplo, al usar 'when' con objetos de tipo Color, podemos determinar un valor basado en su enumeración (enumValue), como 'getMnemonic(Color.BLUE)', que retornará 'Battle'.

También puede aplicarse a otros tipos de objetos o combinaciones, como:
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
> [!NOTE]
> `setOf()` crea conjuntos de colecciones, donde el orden no importa. Esto es útil para comparar conjuntos como colores ( Utilizar condicionales puede ser más eficiente que instanciar objetos para compararlos ).

### _Bucles ( for & while )_
En Kotlin, la estructura `for` se puede emplear de manera similar a Java, pero con una ventaja adicional: puede iterar sobre cualquier objeto que implemente un método `iterator()`. Por ejemplo:
```kotlin
for (c in "abc") {
  print(c + 1)
}
```
Itera sobre cada carácter de "abc" e imprime el siguiente carácter en el alfabeto.

En Kotlin, los bucles while y do-while son similares a los de Java y se usan para ejecutar código mientras se cumple una condición. Por ejemplo:
```kotlin
var x = 10
while (x > 0) {
  x--
}

do {
  val y = retrieveData()
} while (y != null)
```
En este caso, el bucle while decrementa el valor de x hasta que sea igual a 0, mientras que el bucle do-while ejecuta el bloque de código al menos una vez y luego comprueba la condición para decidir si se debe continuar o no.

## Cast en kotlin
En Kotlin, `is` verifica la instancia de un objeto y `as` realiza conversiones de tipo. `is` es similar a `instanceof` en Java y `as` se usa para conversiones de tipo, como un cast en Java. Kotlin también tiene `"smart cast"` para conversiones seguras entre tipos, especialmente en variables inmutables. Por ejemplo:
```kotlin
val n = e as Num
```
Aquí, `'e'` se convierte a tipo `Num` usando `as`

## Rangos
En Kotlin, se pueden usar rangos como en Python. Por ejemplo:
```kotlin
for (i in 1..100) { ... } // es un rango que incluye del 1 al 100.
for (i in 1 until 100) { ... } //es un rango que va del 1 al 99 (sin incluir el 100).
for (x in 2..10 step 2) { ... } // es un rango del 2 al 10 con incrementos de 2.
for (x in 10 downTo 1) { ... } // es un rango del 10 al 1 en orden descendente.
if (x in 1..10) { ... } // verifica si x está dentro del rango del 1 al 10.
```

## Excepciones ( Try catch )
En Kotlin, el manejo de excepciones es similar a Java, pero sin la necesidad de especificar las excepciones que puede lanzar un método. Además, no se requiere el uso de "throws" en la firma del método. 

> [!NOTE]
> Kotlin ofrece flexibilidad al instanciar objetos de excepción y lanzarlos sin necesidad de "new".

> [!IMPORTANT]
> El bloque "try-catch" en Kotlin es una expresión, lo que significa que puede usarse en asignaciones y, si no tiene un cuerpo "{}", devuelve el último valor de la expresión.

Por ejemplo:
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
```

## Exportaciones e importaciones

En Kotlin, puedes exportar e importar tanto paquetes como directorios de una manera similar a Java. Sin embargo, la diferencia radica en que en Kotlin puedes importar de manera más específica.

A continuación observemos un ejemplo:
```kotlin
package geometry.example
import geometry.shapes.createRandomRectangle
```