# Android Development Patterns - Cap 2

## Indice

1. [Unit Testing](#unit-testing)
2. [Integration Testing](#integration-testing)
3. [Debugging](#debugging)

_La realización de pruebas y la depuración son fundamentales en el desarrollo para Android. Estas etapas garantizan la fiabilidad, confiabilidad y mantenibilidad de la aplicación._

## Unit Testing
Es considerado como un testing esencial por muchos desarrolladores, ya que permite conocer el comportamiento y capacidades del código, garantizando su confiabilidad. 

>[!NOTE]
> Por lo general, se escriben pruebas específicas para módulos del código, ya sea clases completas o funciones individuales. Es fundamental adoptar principios de diseño orientado a pruebas al escribir las pruebas unitarias.

Estas son cruciales más allá de garantizar la funcionalidad del código, especialmente en proyectos de colaboración. Sin pruebas adecuadas, surgen conflictos durante la colaboración, lo que retrasa los proyectos. Al proporcionar pruebas junto con el código, los desarrolladores pueden demostrar cómo se prueban los módulos, lo que facilita la comprensión y la colaboración.


![Static Badge](https://img.shields.io/badge/Anotaciones_de_testeo%20-%236A95D6%20?style=for-the-badge)

`@Before:` Se usa para configurar operaciones que se ejecutan al inicio de cada prueba.

`@After:` Se utiliza para ejecutar código al final de cada prueba, generalmente para limpiar recursos en memoria.

`@BeforeClass:` Específico para métodos estáticos que se ejecutan una vez por clase de prueba, útil para operaciones costosas como conexiones a bases de datos.

`@AfterClass:` Similar a @BeforeClass pero se ejecuta después de todas las pruebas, usado para liberar recursos definidos anteriormente.

`@Test:` Marca un método como un caso de prueba.

`@Test(timeout=<milisegundos>):` Define un límite de tiempo para una prueba, considerándola fallida si excede el tiempo especificado.


## Integration Testing
Las pruebas de integración siguen a las pruebas unitarias e implican probar secuencias completas de eventos, componentes de interfaz de usuario e interacciones con proveedores de servicios. Un método de pruebas de integración es utilizar monkeyrunner, una herramienta que ejecuta secuencias de comandos Python para realizar acciones como abrir aplicaciones, enviar eventos de teclado y táctiles y realizar capturas de pantalla en dispositivos Android a través de la conexión ADB.


## ++ Debugging --
Los desarrolladores dedican tiempo a escribir pruebas para garantizar la estabilidad de las aplicaciones. Sin embargo, en Android, a veces las pruebas no funcionan de manera consistente en diferentes dispositivos, lo que requiere depuración. Esto implica perfiles, rastreo y mensajes para identificar y solucionar problemas.

### ++ _Profiling_ --

Al trabajar con una aplicación en Android, es importante conocer cuánta memoria está disponible y cuánta está utilizando tu aplicación. La flexibilidad de Android ha llevado a que muchos fabricantes modifiquen la interfaz de usuario, añadiendo efectos especiales, nuevas aplicaciones y funcionalidades extendidas, lo que puede impactar el rendimiento. Es crucial también considerar el uso de la CPU, ya que cada ciclo consumido implica consumo de energía. Para perfilar tu aplicación, necesitas iniciar el emulador o conectar un dispositivo Android con Depuración USB activada.

### ++ _Tracing_ --
Para rastrear el funcionamiento de tu código, puedes utilizar una utilidad de trazado a nivel del sistema llamada Systrace, que recopila información sobre las aplicaciones en ejecución, el uso de memoria y más. Al completarse, Systrace genera un informe HTML que puede ser visualizado en un navegador web. Esta herramienta es poderosa y proporciona una gran visión sobre lo que tu aplicación y dispositivo están haciendo. 

>[!NOTE]
> Otra forma de depurar tu código implica insertar mensajes de salida de depuración mientras la aplicación está en ejecución. 


### ++ _Menssaging_ --
Diferentes lenguajes de programación ofrecen métodos para enviar mensajes a la consola o depurar registros durante la ejecución del programa. Los ejemplos incluyen alert() y console.log() para desarrolladores web, System.out.println() para desarrolladores de Java y la clase Log en Android para mensajes visibles a través de LogCat. Con la herramienta de línea de comandos adb logcat, los desarrolladores pueden monitorear mensajes en dispositivos o emuladores conectados, con opciones para personalizar la salida.

![Static Badge](https://img.shields.io/badge/The_adb_logcat_Options%20-%23FACA89?style=for-the-badge)

- `-c` borra el registro y sale.
- `-d` muestra el registro en la línea de comandos y luego sale.
- `-f <filename>` permite especificar un archivo para guardar la salida.
- `-g` muestra información sobre el búfer de registro y luego sale.
- `-n <number>` establece cuántos registros rotados mantener.
- `-r <kbytes>` establece el valor de tamaño para un registro antes de rotarlo.
- `-s` filtra el registro al nivel de silencio.
- `-v <format>` establece el formato utilizado para la salida del registro, con opciones como "brief", "process", "tag", "raw", "time", "threadtime" y "long".
