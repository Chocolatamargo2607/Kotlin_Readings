# Android Development Patterns - Cap 9

## Indice

1. [Drawing and Animation](#drawing-and-animation)
2. [Graphics](#graphics)
    - [Bitmaps](#bitmaps)
    - [NinePatch](#ninepatch)
    - [Drawables](#drawables)
    - [OpenGL ES](#opengl-es)
3. [Animation](#animation)
    - [View Animation](#view-animation)
    - [Property Animation](#property-animation)
    - [Drawable Animation](#drawable-animation)
    - [Transition Framework](#transition-framework)



## Drawing and Animation

Más allá del código, es crucial tener un atractivo visual que capture la atención de los usuarios y les brinde algo con lo que interactuar durante las transiciones y eventos de carga
## Graphics
ya sea a través de mapas de bits o mediante OpenGL ES para crear texturas y formas.

### Bitmaps
Son colecciones de información de píxeles que se utilizan para construir imágenes, comúnmente como iconos y recursos de imagen.

Tipos de archivo admitidos:
PNG, JPEG y GIF

>[!IMPORTANT]
Es importante escalar las imágenes antes de cargarlas para evitar problemas de memoria y posibles bloqueos de la aplicación.


Tipos de escalado disponibles
- CENTER
- CENTER_CROP
- CENTER_INSIDE
- FIT_CENTER
- FIT_END
- FIT_START
- FIT_XY
- MATRIX

### NinePatch
Es una imagen hecha a partir de un mapa de bits que puede estirarse al ser mostrada.

>[!IMPORTANT]
Los archivos NinePatch no tienen que ser perfectamente cuadrados; pueden ser rectángulos, círculos e incluso contener áreas con una imagen o logo que no se estirarán.

Permite crear botones y fondos personalizados que se ajusten al tema de la aplicación y sean del tamaño más pequeño posible mientras funcionan en tantas pantallas diferentes como sea posible.

- Para crear un archivo NinePatch, se puede usar la herramienta Draw 9-patch incluida en el SDK de Android.
	- "muestra la imagen original y ayuda a determinar las secciones repetibles y no repetibles".

### Drawables
Son recursos que pueden ser dibujados en la pantalla y pueden ser tanto objetos integrados en Android como recursos que creas tú mismo.


>[!NOTE]
 Algunos drawables, como las formas primitivas, no requieren un archivo en ese directorio(res/drawable), permitiendo crear visualizaciones desde código.

- Se pueden definir en XML utilizando el elemento `<shape>`, permitiendo definir formas como óvalos o círculos con colores y estilos específicos.

>[!NOTE]
Los drawables del sistema permiten que la aplicación se ajuste al tema del sistema, pero pueden ser problemáticos si no se usan adecuadamente. 

### OpenGL ES
Mejor conocido como OpenGL for Embedded Systems es una especificación de la `API` gráfica diseñada para sistemas embebidos, como dispositivos móviles, consolas de videojuegos y otros dispositivos con recursos limitados.

Este ha sido implementado en Android desde la version 1.0 (No todas las versiones son compatibles con Android)

## Animation

### View Animation
Se utilizan cuando se tienen dos vistas y se desea animar entre ellas.
- La animacion de vistas se encarga de todo el cálculo y dibujo para manejar suavemente los cambios en las vistas.

>[!NOTE]
Incluso si no se está construyendo una transición completa, se necesitan los llamados '"tween frames"' para animar una sola vista con cambios como escala, rotación y traslación. 


>[!IMPORTANT]Para crear una animación de vista, se puede usar un archivo XML que contenga los detalles de la animación o las clases AnimationSet y Animator para definir una animación con Java.En el XML de animación, se define un elemento `<set>` que contendrá subelementos para empezar a definir una animación. 


Efectos básicos de animación que se pueden usar: 
- alpha (opacidad o visibilidad)
- rotate (grados de rotación)
- scale (tamaño)
- translate (posición en los planos X y Y).


Un ejemplo de XML de animación sería:

``` kotlin
<scale
 android:interpolator="@android:anim/accelerate_decelerate_interpolator"
 android:fromXScale="1.0"
 android:toXScale="1.5"
 android:fromYScale="1.0"
 android:toYScale="0.5"
 android:pivotX="50%"
 android:pivotY="50%"
 android:fillAfter="false"
 android:duration="800" />
```
"El elemento `<scale>` indica que esta animación escalará lo que se use con ella, y las propiedades listadas controlan la escala."

>[!NOTE]
Si se desea realizar más de una animación, se puede utilizar un elemento <set> y anidar más elementos <set> para ejecutar animaciones en secuencia o al mismo tiempo.

### Property Animation
Permite animar propiedades de cualquier objeto, incluyendo vistas, abriendo nuevas posibilidades como animar propiedades como texto y color de fondo.(Es similar a las animaciones de vista)

se pueden usar archivos XML para definir Property Animations, colocándolos en el directorio res/animator.Para llamar la animación definida en XML, se infla el XML en un objeto AnimatorSet y se usa setTarget() para adjuntar la animación a un objetivo.

>[!NOTE]
Aunque el archivo XML está en res/animator, se usa R.anim.property_animator para cargarlo, debido a la estructura del editor de diseño del antiguo plugin Eclipse ADT.

subclases de la clase Animator que se utilizan para ajustar y crear Property Animations: 
- ValueAnimator
- ObjectAnimator
- AnimatorSet.

`ValueAnimator:` Permite cambiar los valores de un objeto estableciendo un valor inicial y final, una duración y luego iniciando la animación. 
`
ObjectAnimator:` Permite apuntar directamente a una propiedad de un objeto, a diferencia de ValueAnimator. 

En un ejemplo, un ObjectAnimator ajusta la propiedad "alpha" de "myObject" a 0 (no visible) en 1.5 segundos.

`AnimatorSet:` Combina animaciones para cambiar propiedades simultáneamente o en secuencia. Se pueden agregar múltiples animaciones ObjectAnimator a un conjunto. 

### Drawable Animation

Una animación drawable es como crear un libro de animaciones o incluso un GIF animado. Se compone de una lista de drawables que se reproducirán frame por frame. 

>[!NOTE]
Estos recursos se agrupan en un elemento <animation-list> en un archivo XML que se almacena en el directorio /res/drawable de tu proyecto. 

- Para utilizar esta animación en tu código, primero se referencia el archivo XML durante el método onCreate(). Luego, puedes invocar la animación de varias maneras, incluyendo en un evento onTouchEvent.

En si se compone de una serie de drawables que se reproducen secuencialmente, y se pueden controlar fácilmente desde el código de la aplicación, permitiendo crear efectos visuales atractivos y dinámicos.

### Transition Framework

Añadido en la versión 4.4, permite a los desarrolladores crear escenas que luego pueden ser transicionadas. Esto es útil cuando se tienen dos jerarquías de vistas diferentes entre las que se desea cambiar.

Para lograrlo, se usan los diseños de inicio y fin como escenas y luego se aplica una transición a través de TransitionManager.

En lugar de utilizar tres archivos XML de diseño diferentes, se asigna un ID de `scene_container` al `RelativeLayout` para indicar que este es el elemento contenedor que contendrá las escenas transicionadas.

El código necesario para configurar las escenas y realizar la transición es el siguiente:

``` kotlin
Scene mySceneA;
Scene mySceneB;

@Override
protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(R.layout.scene_a);
    
    RelativeLayout mySceneRoot = (RelativeLayout)findViewById(R.id.scene_container);
    mySceneA = Scene.getSceneForLayout(mySceneRoot, R.layout.scene_a, this);
    mySceneB = Scene.getSceneForLayout(mySceneRoot, R.layout.scene_b, this);
    
    Button button = (Button)findViewById(R.id.button);
    button.setOnClickListener(new View.OnClickListener() {
        @Override
        public void onClick(View v) {
            TransitionManager.go(mySceneB);
        }
    });
} 

```
>[!NOTE]
Cuando se ejecuta este código, se ejecutará la transición predeterminada, que puede variar según la versión de Android utilizada, pero generalmente se trata de una transición de desvanecimiento hacia afuera y luego hacia adentro.	

Al usar un transitionSet en un archivo XML de transición, se pueden aplicar múltiples transiciones. El siguiente es un ejemplo de un archivo XML de transición que reside en res/transitions/transition_fader.xml en su proyecto:

```kotlin
<transitionSet xmlns:android="http://schemas.android.com/apk/res/android"
    android:transitionOrdering="sequential">
    <fade android:fadingMode="fade_out" />
    <changeBounds />
    <fade android:fadingMode="fade_in" />
</transitionSet>
```

>[!NOTE]
Esta transición se ejecutará de forma secuencial (gracias a la configuración android:transitionOrdering="sequential") y desvanecerá los elementos, aplicará cambios de propiedades y luego desvanecerá los elementos de nuevo.

Si decide usar un archivo XML para su transición, deberá inflarlo en su código. Esto se puede hacer de la siguiente manera:

```kotlin
Transition myTransitionFader = TransitionInflater.from(this)
    .inflateTransition(R.transition.transition_fader)
```
Ahora que las escenas y la transición han sido definidas, puede iniciar la transición con el siguiente código:

```kotlin
TransitionManager.go(mySceneB, myTransitionFader);
```
Este proceso permitirá cambiar entre las escenas definidas de manera fluida y con las transiciones especificadas.
