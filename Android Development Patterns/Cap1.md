# Android Development Patterns - Cap 1

## Indice

1. [Android Studio](#android-studio)
2. [Version-Control Systems](#version-control-systems)

## Android Studio
En el Google I/O developer conference se anunció Android Studio, una nueva herramienta diseñada para el desarrollo de aplicaciones Android en comparación con el paquete ADT que reemplazó, llevando en principio el facilitar ,acelerar y mejorar el desarrollo en si.

Android Studio esta basado en la plataforma JetBrains IntelliJ IDEA, ofreciendo nuevas caracteristicas interesantes como:

- El guardado automático en cada pulsación de tecla
- La capacidad de separar el proceso de compilación de la aplicación 
- Función de auto-completado inteligente
- Instalación individual para una integración más estrecha con el sistema operativo.

Android Studio está disponible para:

![Static Badge](https://img.shields.io/badge/Windows%20-%2354C6B8?style=for-the-badge)
![Static Badge](https://img.shields.io/badge/Linux%20-%23C398C8?style=for-the-badge)
![Static Badge](https://img.shields.io/badge/OS_X%20-%2383BD86?style=for-the-badge)

>[!NOTE]
> No es necesario utilizar Android Studio para desarrollar aplicaciones Android. Existen otros IDEs disponibles, y algunos IDEs ofrecen un plugin de Android que se encargará de compilar y publicar una aplicación, siempre que tenga acceso al SDK de Android.

### _Emuladores_
Los desarrolladores de aplicaciones para Android enfrentan el desafío de probar sus productos en una amplia variedad de dispositivos, lo cual es prácticamente imposible de lograr físicamente. Aquí es donde los emuladores de Android son fundamentales, ya que permiten a los desarrolladores obtener una idea aproximada del rendimiento y simular el funcionamiento de sus aplicaciones en diferentes versiones de Android.

## Version-Control Systems
El uso de un repositorio de código es fundamental para los desarrolladores, aunque algunos solo lo comprenden tras una falla en el disco duro o un accidente. Existen varias opciones como CVS, SVN, Git, Mercurial, entre otros, para almacenar y gestionar el código, especialmente en el desarrollo de aplicaciones Android.

_Git:_

- ■ Distributed repositories through cloning
- ■ Command-line and client access
- ■ Forking projects
- ■ Ignore file list through .git configuration
- ■ Context switching
- ■ Branching

_Subversion:_

- ■ Ignore file list managed with an .svnignore file
- ■ Branches
- ■ Versioning
- ■ Merge tracking
- ■ Tagging
- ■ Command-line and client access

_Mercurial:_

- ■ Distributed repositories
- ■ Branching
- ■ Merging
- ■ Workflows