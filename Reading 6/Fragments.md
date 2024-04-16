# Fragments in kotlin

## Indice

1. [¿Que es un fragmento?](#¿que-es-un-fragmento)
2. [Ventajas de los fragmentos](#ventajas-de-los-fragmentos)
3. [Creación de un fragmento](#creación-de-un-fragmento)
4. [Atributos del fragmento](#atributos-del-fragmento)
5. [Métodos del fragmento](#métodos-del-fragmento)
6. [Administración de fragmentos](#administración-de-fragmentos)
7. [Comunicación entre fragmentos y actividades](#comunicación-entre-fragmentos-y-actividades)

## ¿Que es un fragmento?

Es una parte reutilizable de la interfaz de usuario (IU), que es capaz de definir y gestionar su propio diseño y eventos de entrada. Sin embargo, por sí solas, estas partes no pueden funcionar, ya que requieren ser alojadas por una actividad u otro fragmento para desplegarse y ejecutarse correctamente.

## Ventajas de los fragmentos
Los fragmentos ofrecen ventajas como:
- La reutilización en distintas actividades
- La modularidad al dividir la interfaz de usuario en partes manejables, modificando la apariencia de la actividad en tiempo real o de ejecución
- La capacidad de escalar aplicaciones de manera compleja.


## Creación de un fragmento
Para generar un fragmento, necesitas desarrollar una clase que herede de la clase Fragment. Esta clase del fragmento debe incluir implementaciones para los siguientes métodos:

- `onCreateView():` Este método se ejecuta cuando el fragmento está siendo creado por primera vez. Su propósito es construir la vista del fragmento.

- `onAttach():` Este método es invocado cuando el fragmento está siendo adjuntado a una actividad. Su objetivo es establecer la actividad anfitriona del fragmento.

- `onDetach():` Este método es llamado cuando el fragmento se está desvinculando de una actividad. Su función es realizar las operaciones necesarias al desprenderse del ciclo de vida de la actividad.

## Atributos del fragmento
Los fragmentos ofrecen una variedad de atributos que permiten ajustar su funcionamiento.

Algunos atributos comunes son:

1. `android:layout_width:` Define el ancho del fragmento.

2. `android:layout_height:` Especifica la altura del fragmento.

3. `android:id:` Identifica de manera única al fragmento.

4. `android:name:` Asigna un nombre al fragmento.

## Métodos del fragmento
Los fragmentos, componentes clave en el desarrollo de aplicaciones Android, no solo ofrecen flexibilidad en la creación de interfaces de usuario, sino que también proporcionan una serie de métodos para interactuar tanto con la interfaz de usuario como con el sistema subyacente.

Algunos de estos métodos comunes incluyen:

- `findViewById():` Una herramienta fundamental para acceder a vistas específicas dentro del fragmento, permitiendo así la manipulación y personalización de elementos visuales.

- `getActivity():` Retorna la actividad que actúa como anfitriona del fragmento, lo que facilita la comunicación y el intercambio de datos entre el fragmento y su actividad principal.

- `setArguments():` Esta función permite establecer argumentos para el fragmento, lo que resulta útil para pasar información entre distintos componentes de la aplicación y mantener un diseño modular y desacoplado.

## Administración de fragmentos
Las actividades en Android tienen la capacidad de gestionar fragmentos, que son componentes modulares de la interfaz de usuario, mediante los siguientes métodos:

- `add():` Este método agrega un fragmento a la actividad. Al utilizar este método, el fragmento se añade encima de cualquier otro contenido presente en la actividad, lo que significa que múltiples fragmentos pueden coexistir en la misma actividad.

- `remove():` Este método elimina un fragmento específico de la actividad. Al llamar a este método, el fragmento seleccionado se elimina de la jerarquía de vistas de la actividad, liberando los recursos asociados a él.

- `replace():` Este método reemplaza un fragmento por otro en la actividad. Al utilizar este método, un fragmento existente se sustituye por otro nuevo. Esto puede ser útil, por ejemplo, para cambiar dinámicamente el contenido de una parte de la interfaz de usuario de la actividad.

Estos métodos ofrecen a los desarrolladores un alto grado de flexibilidad y control sobre la disposición y el comportamiento de los fragmentos en una actividad en una aplicación Android.

## Comunicación entre fragmentos y actividades
Los fragmentos y las actividades pueden comunicarse entre sí utilizando los siguientes métodos:

- `onAttach():` Llamado cuando el fragmento se adjunta a una actividad.

- `onDetach():` Llamado cuando el fragmento se desprende de una actividad.

- `onCreate():` Llamado cuando el fragmento se crea por primera vez.

- `onDestroy():` Llamado cuando el fragmento se destruye.

- `onPause():` Llamado cuando el fragmento se pausa.

- `onResume():` Llamado cuando el fragmento se reanuda.