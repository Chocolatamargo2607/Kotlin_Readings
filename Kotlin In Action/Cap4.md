# KOTLIN IN ACTION - Cap 4

## Indice

1. [Interfaces](#interfaces)
2. [Clases selladas](#clases-selladas)
3. [Clases internas y anidadas](#clases-internas-y-anidadas)
4. [Modificadores de Acceso, Herencia & Visibilidad](#modificadores-de-acceso-herencia--visibilidad)
5. [Constructores](#constructores)
6. [Métodos del Compilador](#métodos-del-compilador)



## Interfaces
En Kotlin, las interfaces son similares a las de Java, pueden contener métodos abstractos y con implementación predeterminada, pero no pueden tener estado. 

>[!IMPORTANT]
> Para declarar una interfaz en Kotlin, se usa la palabra clave `"interface"`, y las clases que las implementan deben proveer implementaciones para todos los métodos abstractos, utilizando "override".

```kotlin
interface Clickable {
    fun click()
    fun showOff() = println("¡Soy clickable!")
}

class Button : Clickable {
    override fun click() = println("Fui clickeado")
}
```
En el ejemplo,una interfaz llamada Clickable tiene dos métodos: uno abstracto `"click"` y otro con una implementación predeterminada `"showOff"`. La clase `Button` implementa esta interfaz y proporciona su propia implementación para el método click. 

>[!NOTE]
> Si una clase implementa múltiples interfaces con métodos de mismo nombre, se utiliza `'super'` con el nombre de la interfaz para invocar una implementación específica.

```kotlin
class Button : Clickable, Focusable {
    override fun click() = println("Fui clickeado")
    override fun showOff() {
        super<Clickable>.showOff()
        super<Focusable>.showOff()
    }
}
```
En este caso, la clase Button implementa tanto Clickable como Focusable, ambas con el método showOff.

>[!NOTE]
>Dentro de la implementación de Button, se llama a los métodos showOff de las clases heredadas utilizando super.

>[!IMPORTANT]
> En kotlin, las clases abstractas se declaran con la palabra clave "abstract" y pueden contener métodos abstractos, es decir, métodos sin implementación. Las clases que heredan de una clase abstracta deben implementar todos sus métodos abstractos.

## Clases selladas
Las clases selladas en Kotlin permiten definir jerarquías de clases restringidas, útiles para manejar todos los subtipos en una expresión `'when'`, sin necesidad de agregar siempre una rama `'else'`debido a que se conoce que solo hay un conjunto limitado de subtipos. Ademas de que garantizan que solo los subtipos directos definidos en la clase sellada puedan existir o puedan ser manejados explícitamente en las expresiones "when".

```kotlin
fun eval(e: Expr): Int = when (e) {
    is Expr.Num -> e.value
    is Expr.Sum -> eval(e.left) + eval(e.right)
}
```
>[!NOTE]
>Aquí no se necesita un "else" ya que todas las opciones están cubiertas por los subtipos de Expr.

Para definir una clase sellada, marca la clase base con `"sealed"` .Los subtipos directos se definen como clases anidadas dentro de la clase base. Por ejemplo `Expr` es una clase sellada con dos subtipos directos: `Num` y `Sum`, los cuales están definidos dentro de la clase sellada, impidiendo la creación de subtipos adicionales fuera de ella.

```kotlin
sealed class Expr {
    class Num(val value: Int) : Expr()
    class Sum(val left: Expr, val right: Expr) : Expr()
}
```

## Clases internas y anidadas
Puedes declarar clases dentro de otras clases. Esto es útil para encapsular clases auxiliares o colocar el código cerca de su uso. Sin embargo, las clases anidadas en Kotlin no tienen acceso a la instancia de la clase externa a menos que lo solicites específicamente.

Esto es importante en situaciones donde deseas definir un elemento de vista `(View)` cuyo estado se pueda serializar. Puedes copiar los datos necesarios a otra clase auxiliar, utilizando métodos como getCurrentState y restoreState para guardar y restaurar el estado de la vista.

```kotlin
interface State : Serializable

interface View {
    fun getCurrentState(): State
    fun restoreState(state: State) {}
}
```
Por defecto, una clase anidada en Kotlin es estática, a diferencia de Java. Para hacerla interna y acceder a la clase externa, se utiliza el modificador "inner". La sintaxis para referenciar una instancia de la clase externa es this@Outer en Kotlin. Por ejemplo:

```kotlin
class Outer {
    inner class Inner {
        fun getOuterReference(): Outer = this@Outer
    }
}
```

## Modificadores de Acceso, Herencia & Visibilidad
En Kotlin, los modificadores de acceso y herencia son clave para estructurar jerarquías de clases y proteger los miembros de las mismas.

### _Acceso_

- `public:` Miembros accesibles desde cualquier lugar fuera de la clase.
```kotlin
class MiClase {
    public val miVariable = 42
}

```
- `internal:` Accesible solo dentro del módulo actual para ocultar detalles de implementación de otros módulos.
```kotlin
internal class MiClaseInternal {
    internal val miVariable = 42
}

```
- `protected:` Accesible solo dentro de la clase y en sus subclases.
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
- private: Solo accesible dentro de la clase que los define.
```kotlin
class MiClasePrivada {
    private val miVariable = 42
}

```

### _Herencia_

- `Final:` Impide la herencia o sobrescritura de una clase o método.
```kotlin
open class ClaseBase {
    final fun metodoFinal() {}
}

class SubClase : ClaseBase() {
    // Error: No se puede sobrescribir un método final
    // override fun metodoFinal() {}
}
```open class ClaseBase {
    final fun metodoFinal() {}
}

class SubClase : ClaseBase() {
    // Error: No se puede sobrescribir un método final
    // override fun metodoFinal() {}
}
- `Open:` Permite la herencia o sobrescritura de una clase o método, debe usarse explícitamente.
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
- `Abstract:` Define métodos abstractos en una clase que deben ser implementados en las subclases.
```kotlin
abstract class ClaseAbstracta {
    abstract fun metodoAbstracto()
}
```
- `Override:` Indica que una función o propiedad está sobrescribiendo un miembro de una superclase o interfaz.
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
>[!NOTE]
> Estos modificadores aseguran un código más seguro y estructurado en Kotlin.

### _Visibilidad_
controlan el acceso a las declaraciones. Son similares a los de Java, pero la visibilidad predeterminada es public en lugar de package-private. Además, Kotlin introduce el modificador internal para "visible dentro de un módulo". Por ejemplo:

```kotlin
internal open class TalkativeButton : Focusable {
    private fun yell() = println("Hey!")
    protected fun whisper() = println("Let's talk!")
}

fun TalkativeButton.giveSpeech() {
    yell() // Esto genera un error, ya que yell() es privado
    whisper()
}

En este ejemplo, `TalkativeButton` es internal, `yell()` es privada y `whisper()` es protegida. La función `giveSpeech()` intenta acceder a `yell()`, lo que genera un error de compilación. Los modificadores de visibilidad en Kotlin permiten un control preciso sobre el acceso a las declaraciones.

```
## Constructores
En Kotlin, los constructores pueden ser primarios o secundarios.

Constructor primario: Se define junto con la declaración de la clase principal y se usa para inicializar propiedades y recibir parámetros al crear una instancia de la clase.

```kotlin
class User(val nickname: String)
```
Constructores secundarios: Se definen en la clase con la palabra clave constructor y son útiles para proporcionar diferentes formas de inicializar un objeto. Puedes tener múltiples constructores secundarios en una clase.

```kotlin
class User(val nickname: String) {
    constructor(email: String, password: String) : this(email.split("@")[0])
}
```
>[!NOTE]
> Estos constructores secundarios pueden tener diferentes parámetros o lógica de inicialización según sea necesario.

Debemos de tener en cuenta que los constructores pueden tener valores predeterminados para los parámetros, lo que permite crear instancias de la clase sin necesidad de proporcionar todos los parámetros. Por ejemplo:

```kotlin
class User(val nickname: String, val Subscribed: Boolean = true)
```
Aquí, `Subscribed` tiene un valor predeterminado, el cual es `true`, por lo que al crear un usuario sin especificar este parámetro, se asume inmediatamente el valor que posea por predeterminado.


## Métodos del Compilador
En Kotlin, el compilador genera métodos comunes como equals, hashCode y toString automáticamente, simplificando el manejo de clases de datos y la delegación de métodos. Aquí están los conceptos principales:

1. `toString():` Obtiene una representación de cadena de un objeto.
```kotlin
data class Persona(val nombre: String, val edad: Int)

fun main() {
    val persona = Persona("Juan", 30)
    println(persona.toString()) // Imprime: Persona(nombre=Juan, edad=30)
}
```

2. `equals():` Define la comparación entre dos objetos.
```kotlin
data class Punto(val x: Int, val y: Int)

fun main() {
    val punto1 = Punto(1, 2)
    val punto2 = Punto(1, 2)
    println(punto1 == punto2) // Imprime: true
}
```

3. `hashCode():` Calcula un valor numérico que representa un objeto.

```kotlin
data class Estudiante(val id: Int, val nombre: String)

fun main() {
    val estudiante1 = Estudiante(1, "Ana")
    val estudiante2 = Estudiante(1, "Ana")
    println(estudiante1.hashCode() == estudiante2.hashCode()) // Imprime: true
}

```
>[!NOTE]
> Dos objetos iguales deben tener el mismo valor de hash.


4. `Data class:` Simplifica la creación y manejo de objetos de datos.
```kotlin
data class Producto(val nombre: String, val precio: Double)

fun main() {
    val producto = Producto("Laptop", 1200.0)
    println(producto) // Imprime: Producto(nombre=Laptop, precio=1200.0)
}
```

5. `Delegación de Clases:` Utiliza la palabra clave 'by' para delegar la implementación a otra clase.
```kotlin
interface Vehiculo {
    fun conducir()
}

class Coche : Vehiculo {
    override fun conducir() {
        println("Conduciendo el coche...")
    }
}

class Conductor(vehiculo: Vehiculo) : Vehiculo by vehiculo

fun main() {
    val coche = Coche()
    val conductor = Conductor(coche)
    conductor.conducir() // Imprime: Conduciendo el coche...
}
```

6. `Companion Objects:` Define métodos de fábrica y miembros estáticos.
```kotlin
class Circulo(val radio: Double) {
    companion object {
        fun crearCirculo(radio: Double): Circulo {
            return Circulo(radio)
        }
    }
}

fun main() {
    val circulo = Circulo.crearCirculo(5.0)
    println("Radio del círculo: ${circulo.radio}") // Imprime: Radio del círculo: 5.0
}
```

7. `Extensiones de Objetos Compañeros:` Permite definir métodos llamables como miembros estáticos.

```kotlin
class Texto(val contenido: String)

fun Texto.imprimir() {
    println(this.contenido)
}

fun main() {
    val texto = Texto("Hola, mundo!")
    texto.imprimir() // Imprime: Hola, mundo!
}
```

8. `Expresiones de Objetos:` Crea objetos anónimos de manera concisa.
```kotlin
interface Animal {
    fun hacerSonido()
}

fun main() {
    val perro: Animal = object : Animal {
        override fun hacerSonido() {
            println("Guau!")
        }
    }

    perro.hacerSonido() // Imprime: Guau!
}
```
