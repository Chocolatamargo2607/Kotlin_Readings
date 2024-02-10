# KOTLIN IN ACTION - Cap 1

## Indice

1. [¿Que es kotlin?](#introduccion)
2. [Principio](#principio)
3. [Caracteristicas](#caracteristicas)
4. [Compilación de kotlin](#compilacion)

## ¿Que es kotlin?
Es un lenguaje de programación moderno o legacy, orientado a objetos con un enfoque funcional.

Kotlin proporciona una alternativa de Java más concisa, productiva y segura, que sea adecuada en todos los contextos en los que se utiliza Java hoy en día. Ademas de que permite a los desarrolladores escribir código de manera más eficiente y menos propensa a errores.

### _Áreas de uso_
![Static Badge](https://img.shields.io/badge/Backend_de_aplicaciones_web%20-%23FA8E5F?style=for-the-badge)
![Static Badge](https://img.shields.io/badge/Microservidores%20-%23FACA89?style=for-the-badge)
![Static Badge](https://img.shields.io/badge/Aplicaciones_multiplataforma%20-%2383BD86?style=for-the-badge)
![Static Badge](https://img.shields.io/badge/Aplicaciones_Moviles%20-%2354C6B8?style=for-the-badge)

### _Plataformas de destino_
![Static Badge](https://img.shields.io/badge/Servidor%20-%236A95D6%20?style=for-the-badge)
![Static Badge](https://img.shields.io/badge/Android_/_IOS%20-%23C398C8?style=for-the-badge)
![Static Badge](https://img.shields.io/badge/Programas_de_uso_en_java%20-%23E891BD?style=for-the-badge)


## Principio
El principio fundamental de Kotlin es la pragmaticidad, puesto que este es un lenguaje práctico que se enfoca en mejorar la productividad de los desarrolladores sin comprometer la interoperabilidad, la seguridad o el rendimiento.

Este fue diseñado para ser `interoperable` con Java, lo que significa que los desarrolladores pueden aprovechar las bibliotecas y herramientas existentes de Java en sus proyectos de Kotlin sin problemas.

## Caracteristicas
### _Tipado estatico_
Kotlin es un lenguaje de tipado estático(el tipo de variable no cambia), pero es flexible al momento de declarar una variable, pues no es necesario decirle que tipo de dato va almacenar dicha variable.

Algunas de ventajas que posee son:
- **Rendimiento**
- **Fiabilidad**
- **Mantenibilidad**
- **Soporte de herramientas**

> [!IMPORTANT]
> Se debe de tener en cuenta que este tipo de lenguaje nos presenta una nueva forma de crear variables

```kotlin    
val a:int? = null 
```
"Donde al añadir el simbolo `?`, declaramos que esta variable puede llegar a poseer un valor nulo (normalmente cuando no se le declara prebiamente un valor especifico). A continuacion se presenta un ejemplo basico frente del manejo de kotlin"

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
    println("The oldest is: $oldest")
  }
```
### _Principio de funcionalidad y orientacion a objetos_
Al escribir el codigo en un estilo funcional, poseemos la capacidad de entregar un codigo mas limpio, consiso, y logramos evitar la duplicacion de codigo.
 
Cuando tienes dos fragmentos de código similares para realizar una tarea común pero con diferencias en los detalles, puedes crear una función que encapsule la lógica común y pasar las diferencias como argumentos, utilizando expresiones lambda para representar funciones anónimas de manera concisa.

```kotlin
fun findAlice() = findPerson { it.name == "Alice" }
fun findBob() = findPerson { it.name == "Bob" }
```
Donde `findPerson()` se encarga de contener la lógica general para encontrar a una persona y el bloque `{}` contiene los detalles de la persona a buscar.

#### Características de kotlin para soportar la programación funcional :

![Static Badge](https://img.shields.io/badge/Functional_types%20-%2383BD86?style=for-the-badge)
![Static Badge](https://img.shields.io/badge/Lambda_expressions%20-%2354C6B8?style=for-the-badge)
![Static Badge](https://img.shields.io/badge/Data_classes%20-%23C398C8?style=for-the-badge)
![Static Badge](https://img.shields.io/badge/Access_to_APIs%20-%23FFFDF9?style=for-the-badge)

## Compilación de kotlin
La compilacion de este lengüaje posee la siguiente serie de pasos.

**1.** El código se almacena en archivos con la extensión .kt

**2.** El compilador analiza el código fuente y genera archivos .class

**3.** Los archivos .class se empaquetan y compilan según el tipo de proyecto, lo que da lugar a la creación del archivo .jar.

```kotlin
kotlinc <source file or directory> -include-runtime -d <jar name>
```

**4.** Se ejecuta el codigo con el comando `java -jar <jar file name>`

**5.** La ejecucion del el Kotlin runtime se hace junto con las bibliotecas de Kotlin, puesto que depende de ellas 

**6.** Finalmente obtenemos el producto, el cual es la aplicacion deseada.

### Graphic description of the construction process
![Imagen](/Imagens/Compilacion.png)
