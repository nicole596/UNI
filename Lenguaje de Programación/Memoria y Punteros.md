# Memoria

## ¿Qué es?

En una computadora la memoria esta organizada en una gran cantidad de bytes. Cada byte puede guardar información y tiene una dirección única.

## Bloque de Memoria

Un bloque de memoria es una sección organizada de bytes en las que no hay espacio desperdiciado. Se usa a menudo para guardar información relacionada entre si, tales como arreglos o cadenas. De esta forma la computadora puede acceder a estos datos de manera mas eficiente.

## Dirección de Memoria


Una dirección de memoria es un identificador único que apunta a un byte en la memoria.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693747295569/8958df47-143a-465c-84f4-223055681b71.png)
### Analogía de la biblioteca

En esta analogía la memoria es una biblioteca con un numero finito de espacios para guardar libros. Cada espacio es un byte con un nombre único para identificarlo. Los libros son la información guardada en el byte. También podemos organizar la biblioteca en categorías, estas serian los bloques de memoria.
# Manejo de Memoria

Al ser C un leguaje de bajo nivel, la memoria se maneja de dos forma diferentes. De mamera automática (stack) o de manera manual (heap).
## Stack

El stack es un bloque de memoria manejado por el compilador de C. Este crece o decrece automáticamente. 

Este tipo de manejo de memoria se rige por el principio Last In - First Out.  Siguiendo con la analogía de la biblioteca, un stack es como una pila de libros, cuando llega un libro puedes agregarlo a la parte superior de la pila (push) o quitar el último libro agregado (pop).

Las variables temporales creadas con este método son destruidos automáticamente cuando el tiempo de ejecución de C termina.

### Stack Pointer

El Stack usa una variable especial llamada Stack Pointer que mantiene un seguimiento de la parte superior del Stack. Cuando llega una nueva variable el Stack Pointer sube y cuando una se va el Stack Pointer baja.

### **Características

- **Fast Allocation/Deallocation**
- **Tamaño predeterminado**
- **Last-In, First-Out (LIFO)**
- **Manejo automático**
- **Alcance local**
### Código

```c
#include <stdio.h>

void myFunction(int param) {
  int localVar = 10;  // localVar is pushed onto the Stack
  printf("Parameter value: %d\n", param);
  printf("Local variable value: %d\n", localVar);
  // Both param and localVar are popped off the 
  // Stack when myFunction returns
}

int main() {
  int mainVar = 5;  // mainVar is pushed onto the Stack
  myFunction(mainVar);  // mainVar is passed as a parameter to myFunction
  // mainVar remains on the Stack until main() returns
  return 0;
  // mainVar is popped off the Stack here
}
```

## Heap

El heap es una región de memoria que no esta manejada automáticamente. Es decir, se mantendrá en la memoria hasta que sea liberada explicitamente

### Heap Pointer

Cuando creas un nuevo bloque de memoria, se genera un puntero que apunta al inicio del bloque.
### **Características

- **Dynamic Size**: The heap grows and shrinks during runtime as required.
    
- **Slower Allocation/Deallocation**: Compared to the stack, heap allocation and deallocation are slower. This is because e.g. allocation on the heap involves finding a block of memory large enough to fit the data, which can take time.
    
- **Explicit Management**: You have to explicitly allocate and deallocate memory.
    
- **Global Scope**: Data in the heap is globally accessible as long as you've a pointer to the data.
    

### Code

```c
#include <stdio.h>
#include <stdlib.h>

void myFunction() {
  int *heapVar = malloc(10 * sizeof(int));  // Allocating an array of 10 ints on the Heap

  if (heapVar == NULL) {  // Always check if malloc succeeded
    printf("Memory allocation failed!\n");
    exit(1);
  }

  heapVar[0] = 42;  // Access heap memory like regular array
  printf("First value in heap array: %d\n", heapVar[0]);

  free(heapVar);  // Don't forget to free the memory!
  // heapVar now dangles, do not use it until you point it to a valid memory location again
}

int main() {
  myFunction();  // myFunction allocates and frees memory on the Heap
  return 0;
}
```

# Pointers

## ¿Qué son?

Los punteros en C son variables que almacenan la dirección de donde se guardan los datos. No contienen los datos en sí, sino que apuntan a ellos.

Piensa en un puntero como el mapa de un tesoro. No contiene el tesoro (los datos). En su lugar, te dice dónde encontrarlo.

```c
#include <stdio.h>

int main() {
    int x = 10;
    int *ptr = &x;
    printf("Value of x: %d\n", *ptr);
    return 0;
}
```

Aquí, `ptr` no contiene el valor (`10`), pero te dice donde encontrar la ubicación en la memoria de `x`.

You turn a variable into a pointer by putting `*` behind it.

Conviertes una variable en un puntero colocando un `*` antes de su nombre en la declaración. Si hiciéramos `int *pointer = x;`, significaría asignar el valor de `x` directamente al puntero, lo cual no funcionaría.

Para obtener la dirección de dónde están almacenados los datos de una variable, se coloca un `&` antes de ella.
## Declarar un puntero vacío

Declarar un puntero vacío es como recibir el mapa de un tesoro en blanco. Todavía no sabes dónde está el tesoro, pero tienes algo para rellenar con los detalles más tarde.

```c
int *ptr1;
float *ptr2;
char *ptr3;
```

## Operadores de Dirección y Des referenciación

El símbolo amperio o et (`&`) para variables que contienen valores es como preguntar: _"¿Dónde queda tu casa?"_. El asterisco (`*`), cuando se usa sobre un puntero, es como ir a esa casa para ver qué hay dentro.

Echemos un vistazo a un poco de código:

``` C
int x = 20;
int *ptr = &x;  // &x significa la "direccion de x"
int y = *ptr;  // *ptr significa "valor en la direccion almacenada en ptr"
```

No te confundas aquí. Estamos usando el `*` otra vez, pero sobre el puntero. Esto se llama **desreferenciación**. Estamos obteniendo el valor al que apunta la dirección del puntero.

## Puntero NULL

El puntero `NULL` es un valor de puntero especial. Significa que el puntero no está apuntando a ninguna ubicación de memoria válida.

Piensa en él como un letrero en medio del desierto que dice: _"No hay nada que ver aquí"_. Al igual que no cavarías en busca de un tesoro en un lugar con ese letrero, no debes buscar datos ahí.

Normalmente usarías punteros `NULL` cuando quieres inicializar un puntero pero aún no tienes una dirección específica a la cual apuntar. Esto asegura que no desreferencies accidentalmente valores basura de la memoria.

``` C
int *ptr = NULL;

if (ptr) { // No se ejecutara porque ptr es NULL
    printf("%d", *ptr);
}
```

## Aritmética de Punteros

La aritmética de punteros te permite mover tu puntero hacia adelante o hacia atrás en la memoria, permitiéndote navegar eficazmente por un arreglo o bloque de memoria.

Imagina que estás leyendo un libro y tu dedo va siguiendo las líneas mientras lees. Puedes mover tu dedo (puntero) hacia adelante a la siguiente palabra o hacia atrás a la palabra anterior. Esto es lo que la aritmética de punteros te permite hacer en la memoria.

La aritmética de punteros es muy útil cuando manejas arreglos y buffers. Te permite recorrer un arreglo sin necesidad de usar un índice. Es importante notar que las cadenas (_strings_) son arreglos de caracteres en C, así que también resulta útil para ellas.

### Arreglos

``` C
#include <stdio.h>

int main() {
    int arr[5] = {1, 2, 3, 4, 5};
    int *ptr = arr;

    // ptr apunta al primer elemento de arr, que es 1
    printf("Primer elemento: %d\n", *ptr);  // Salida: Primer elemento: 1

    // Usando aritmetica de punteros para moverse al siguiente elemento
    ptr += 1;
    printf("Segundo elemento: %d\n", *ptr);  // Salida: Segundo elemento: 2

    return 0;
}
```

Para aclarar: Cuando asignas un arreglo a un puntero, el puntero apunta automáticamente al primer elemento.

### Cadenas (Strings)

``` C
#include <stdio.h>

int main() {
    char str[] = "Hello";
    char *ptr = str;

    // ptr apunta al primer caracter de str, que es 'H'
    printf("Primer caracter: %c\n", *ptr);  // Salida: Primer caracter: H

    // Usando aritmetica de punteros para moverse al siguiente caracter
    ptr += 1;
    printf("Segundo caracter: %c\n", *ptr);  // Salida: Segundo caracter: e

    return 0;
}
```

Como puedes ver, asignar cadenas a un puntero hace que este apunte al primer carácter, es decir, al primer elemento en el arreglo de caracteres.

## ¿printf con *?

Tal vez te confunda ver los ejemplos. ¿Por qué usamos `*ptr` cuando llamamos a `printf`? Tenemos que desreferenciar el puntero. De lo contrario, estaríamos imprimiendo la dirección de memoria física. Pero en los ejemplos, lo que queremos es imprimir los valores almacenados en esas direcciones.
## ¿Qué es exactamente un arreglo?

Un arreglo, como habrás adivinado, es un bloque de memoria. Es una sección de bytes organizados de forma contigua.

## Las cadenas bajo el capó

En nuestro ejemplo anterior, teníamos la cadena `"Hello"`. Por dentro, esto es en realidad un arreglo de caracteres: `{'H', 'e', 'l', 'l', 'o', '\0'}`.

Es posible que te esperaras la mayor parte, excepto el valor del final: `\0`. ¿Qué es esto? En C, las cadenas son arreglos de caracteres y el lenguaje no tiene un tipo de datos "string" nativo como otros lenguajes de programación. Por lo tanto, tenemos el **terminador nulo (\0)**, que sirve como marcador para el final de la cadena, diciéndole a las funciones que procesan cadenas dónde dejar de leer el arreglo de caracteres.

### ¿Pero por qué lo necesitamos?

- **Funciones que procesan cadenas:** Funciones como `strlen()`, `strcpy()` y `strcat()` dependen del terminador nulo para saber cuándo termina la cadena. Sin él, estas funciones seguirían leyendo la memoria indefinidamente hasta encontrar un byte cero aleatorio, lo que podría provocar desbordamientos de búfer (_buffer overflows_), fallos de segmentación (_segmentation faults_) u otros comportamientos indefinidos.
    
- **Corrupción de memoria:** Si el terminador nulo no está ahí, es muy probable que se lea más allá de la memoria válida asignada para la cadena. Esto resultaría en la corrupción de los datos y causaría un comportamiento impredecible del software.
    
- **Riesgos de seguridad:** El comportamiento indefinido asociado con la falta de un terminador nulo puede ser explotado en ataques informáticos, como los ataques de desbordamiento de búfer.

## Punteros y Funciones

Los punteros se pueden pasar a las funciones como argumentos, permitiendo que dichas funciones modifiquen los valores reales a los que apuntan los punteros.

Imagina que le das a alguien el control remoto de tu casa inteligente. Esa persona puede cambiar el termostato, encender y apagar las luces, etc., sin necesidad de estar físicamente dentro de tu casa. Así es exactamente como funciona pasar punteros a funciones.

Los punteros se pasan a menudo a las funciones para modificar directamente las variables de las funciones que las llaman, para devolver múltiples valores o para pasar grandes estructuras de datos de manera eficiente sin tener que copiarlas.


``` C
void modify(int *a) { // La funcion recibe un puntero a `a`.
    *a = 10; // Desreferencia para asignar un nuevo valor a la ubicacion a la que apunta la direccion.
}

int main() {
    int x = 5;
    modify(&x);  // x ahora es 10
    return 0;
}
```

# Punteros a Punteros (Pointers to Pointers)

Una variable que apunta a un puntero. Es decir, una variable que contiene la dirección de otro puntero. Eso es un puntero a un puntero. Se declaran usando un doble asterisco .


``` C
int x = 5;          // Una variable 'x'
int *p = &x;        // Un puntero 'p' que almacena la direccion de 'x'
int **pp = &p;      // Un puntero a un puntero 'pp' que almacena la direccion de 'p'
```

### Analogía

Imagina que tienes un cofre del tesoro (que representa una variable). Dentro de este cofre hay un mapa (puntero) que lleva a otro cofre. Ahora, tienes un tercer cofre que contiene un mapa hacia el cofre que tiene el primer mapa. Este tercer cofre es el puntero a puntero. Te lleva indirectamente al tesoro final (la variable original).

### ¿Por qué demonios necesitamos esto?

Ahora que lo has entendido, probablemente pienses que es una característica innecesaria. No es algo que vayas a usar todos los días. El principio general es: cada vez que necesites un nivel extra de indirección o flexibilidad, considera usar un puntero a un puntero.

> **Dato curioso:** También podrías tener un puntero que apunte a un puntero que apunta a un puntero (un puntero de triple nivel).

``` C
> int x = 5;
> int *p = &x;
> int **pp = &p;
> int ***ppp = &pp; // Un puntero a un puntero a puntero 'ppp' que almacena la direccion de 'pp'
```

### Casos de uso comunes

- **Arreglos bidimensionales (2D) dinámicos:** Cuando quieres un arreglo 2D (como una tabla o cuadrícula) que pueda cambiar de tamaño, usas punteros a punteros. Esto te da un "arreglo de arreglos", y cada fila puede tener un tamaño diferente.
    
- **Análisis de argumentos de la línea de comandos:** Cuando tu programa en C se inicia, recibe sus argumentos de la línea de comandos como una lista de cadenas. En C, esta lista es en realidad un puntero a un puntero (`char argv`). Puedes recorrer esta lista fácilmente para descubrir qué opciones o archivos especificó el usuario.
    
- **Estructuras de datos dinámicas:** Si estás construyendo cosas complejas como árboles o redes de elementos conectados (grafos), a menudo necesitarás punteros a punteros. Esto permite que un nodo se conecte y reasigne fácilmente con otros nodos.
    
- **Cambiar punteros dentro de funciones:** A veces, no solo estás cambiando los datos a los que apunta un puntero, sino que estás cambiando la ubicación a la que apunta el propio puntero. Para hacer esto dentro de una función, necesitarás pasar un puntero a un puntero.
    

## Arreglos 2D

Primero veamos cómo se ven los arreglos 2D tradicionales y fijos:

``` C
#include <stdio.h>

int main() {
    // Declara un arreglo de 3x2. Esto crea un bloque contiguo de memoria.
    int arr[3][2] = {
        {1, 2},  // Primera fila
        {3, 4},  // Segunda fila
        {5, 6}   // Tercera fila
    };

    // Accediendo a los elementos: arr[fila][columna]
    printf("Elemento en (2,1): %d\n", arr[1][0]); // La salida sera 3

    // Bucle anidado para iterar a traves de todos los elementos
    for (int i = 0; i < 3; ++i) {
        for (int j = 0; j < 2; ++j) {
            printf("%d ", arr[i][j]);
        }
        printf("\n");
    }

    return 0;
}
```

Como puedes ver arriba, los arreglos 2D son como filas y columnas. El primer índice es la fila a la que estás accediendo y el segundo es la columna.

Problemas si quieres crear arreglos 2D de tamaño dinámico:

- **Tamaño fijo:** Las dimensiones deben conocerse en el tiempo de compilación, lo que limita si necesitas que cambie de tamaño en tiempo de ejecución.
    
- **Sobrecarga de memoria:** Si asignas un arreglo 2D gigante para prever un tamaño máximo, pero terminas usando solo una fracción de él, estarás desperdiciando memoria.
    
- **Sin filas de longitud variable:** Todas las filas deben tener estrictamente el mismo número de columnas.
    

Veamos cómo crear arreglos 2D de tamaño dinámico usando punteros a punteros:

``` C
#include <stdio.h>
#include <stdlib.h>

int main() {
    // Declara un puntero a un puntero. Servira como nuestro arreglo 2D.
    int **arr;

    // Asigna memoria para 3 punteros (3 filas).
    // Cada uno de estos punteros apuntara a un arreglo (una fila).
    arr = malloc(3 * sizeof(int *));
    if (arr == NULL) {
        return 1;  // Fallo la asignacion de memoria
    }

    // Asigna memoria para cada fila y establece los valores.
    for (int i = 0; i < 3; ++i) {
        // Asigna memoria para 2 enteros en cada fila.
        arr[i] = malloc(2 * sizeof(int));
        if (arr[i] == NULL) {
            return 1;  // Fallo la asignacion de memoria
        }

        // Inicializa los elementos. arr[i][j] = i * j;
        arr[i][0] = i;
        arr[i][1] = i * 10;
    }

    // Accediendo a los elementos: arr[fila][columna]
    // Bucle anidado para iterar a traves del arreglo 2D asignado dinamicamente
    for (int i = 0; i < 3; ++i) {
        for (int j = 0; j < 2; ++j) {
            printf("%d ", arr[i][j]);  // Imprime cada elemento
        }
        printf("\n");
    }

    // Libera cada fila asignada dinamicamente
    for (int i = 0; i < 3; ++i) {
        free(arr[i]);
    }

    // Libera el arreglo que contiene los punteros de las filas
    free(arr);

    return 0;
}
```

Primero asignamos dinámicamente un "arreglo de punteros" (`arr`), y luego, para cada uno de esos punteros, asignamos dinámicamente un arreglo de enteros. Este es un arreglo 2D dinámico completamente bajo tu control.

## Análisis de argumentos de la línea de comandos

Al desarrollar un programa en C, el sistema operativo le pasa los argumentos a tu función `main()`. Esto se hace a través de los parámetros `argc` (conteo de argumentos) y `argv` (arreglo de punteros a cadenas). Sin embargo, este arreglo de punteros se pasa en realidad como un puntero a un puntero (`char argv`).

C

```
#include <stdio.h>

// Nuestra funcion main que recibe los argumentos de la linea de comandos
int main(int argc, char **argv) {
    // Bucle a traves de cada argumento de la linea de comandos
    for(int i = 0; i < argc; i++) {
        // Imprime el argumento
        // argv[i] toma el i-esimo argumento de la linea de comandos
        printf("El argumento %d es %s\n", i, argv[i]);
    }
    return 0;
}
```

Puede parecer confuso que no estemos desreferenciando `argv` con un asterisco antes de acceder al valor. La verdad es que C hace eso por nosotros bajo el capó cuando indexamos un arreglo.

Cuando escribes `argv[i]`, es exactamente lo mismo que `*(argv + i)`. El puntero `argv` se incrementa en `i` posiciones y luego se desreferencia. Así que cuando veas `*(argv + i)`, puedes leerlo de esta manera:

1. _"Toma el puntero argv"_.
    
2. _"Muévete i pasos hacia adelante para apuntar al i-ésimo elemento del arreglo"_.
    
3. _"Ahora desreferencia este nuevo puntero para darme el valor guardado allí"_.
    

## Argumentos de función avanzados

Si pasas un puntero de un solo nivel a una función y lo modificas por dentro (por ejemplo, asignándole memoria con `malloc`), los cambios **no se reflejarán fuera de la función**. Esto sucede porque la función trabaja con una copia local del puntero.

La solución es pasar un **puntero al puntero** como argumento. De esta manera, le das a la función la capacidad de modificar el puntero original.

### Esto NO funcionaría:

C

```
#include <stdio.h>
#include <stdlib.h>

// Funcion para inicializar el arreglo
void initializeArray(int *arr, int size) {
    arr = malloc(size * sizeof(int));  // Asigna memoria
    for (int i = 0; i < size; ++i) {
        arr[i] = i;
    }
}

int main() {
    int *myArray = NULL;  // Declara un puntero a int
    initializeArray(myArray, 5);  // Llama a la funcion para inicializar el arreglo

    if (myArray == NULL) {
        printf("Memoria no asignada.\n");
    }

    return 0;
}
```

### Esto SÍ funcionaría:

C

```
#include <stdio.h>
#include <stdlib.h>

// Funcion para inicializar el arreglo
void initializeArray(int **arr, int size) {
    // Asigna memoria al puntero original apuntado por arr
    *arr = malloc(size * sizeof(int));  
    // Inicializa el arreglo
    for (int i = 0; i < size; ++i) {
        (*arr)[i] = i;
    }
}

int main() {
    int *myArray = NULL;  // Declara un puntero a int
    initializeArray(&myArray, 5);  // Pasa la direccion del puntero para inicializar el arreglo

    // Verifica si la memoria fue asignada y el arreglo fue inicializado
    if (myArray != NULL) {
        for (int i = 0; i < 5; ++i) {
            printf("%d ", myArray[i]);  // Deberia imprimir 0 1 2 3 4
        }
        printf("\n");
    }

    // No olvides liberar la memoria
    free(myArray);

    return 0;
}
```

# Punteros a Funciones (Function Pointers)

Los punteros a funciones en C son una forma de almacenar la dirección de una función en memoria, para que puedas llamarla más tarde o pasarla a otra función como parámetro.

La sintaxis para declarar un puntero a función es:

`tipo_de_retorno (*nombre_del_puntero)(tipo_parametro1, tipo_parametro2, ...);`

Digamos, por ejemplo, que tenemos esta función:

C

```
int add(int a, int b);
```

El puntero a esa función se declararía así:

C

```
int (*add_ptr)(int, int);
```

Puedes inicializarlo usando el operador de dirección `&`:

C

```
add_ptr = &add;
```

Para llamar a la función, desreferencias el puntero:

C

```
int result = (*add_ptr)(5, 3);  // Esto llama a add(5, 3)
```

C también te permite omitir el asterisco al llamarla, lo cual es mucho más limpio y totalmente válido:

C

```
int result = add_ptr(5, 3);  // Esto tambien llama a add(5, 3)
```

### ¿Cuándo los necesitas?

Los punteros a funciones te permiten tratar las funciones como si fueran variables. Se usan a menudo en:

- **Arquitecturas de complementos (Plug-ins):** Para extender funciones sin modificar el código base.
    
- **Programación orientada a eventos:** En entornos gráficos (GUIs) para manejar acciones como clics de botones de forma dinámica.
    
- **Funciones de devolución de llamada (Callbacks):** Como cuando pasas una función de comparación personalizada a un algoritmo de ordenamiento.
    
- **Máquinas de estado:** En sistemas embebidos para representar estados de manera compacta.
    

### Ejemplo del mundo real (Simulación de botones en una GUI)

C

```
#include <stdio.h>

// Definicion del tipo de puntero a funcion para manejar clics de botones.
typedef void (*ButtonClickedHandler)(void);

// Estructura Button, que encapsula los atributos de un boton.
typedef struct {
    ButtonClickedHandler onClick;  // Puntero a funcion para el evento de clic.
    const char* label;  // Texto de la etiqueta en el boton.
} Button;

// Funcion que simula hacer clic en un boton.
void button_click(Button* button) {
    // Verifica si se ha establecido un puntero a funcion.
    if (button->onClick != NULL) {
        printf("Boton '%s' clickeado. ", button->label);
        button->onClick();  // Llama a la funcion a traves del puntero.
    } else {
        printf("Boton '%s' clickeado pero no tiene accion asignada.\n", button->label);
    }
}

// Una funcion personalizada que se llamara cuando se haga clic.
void say_hello() {
    printf("¡Hola, Mundo!\n");
}

// Otra funcion personalizada para otro boton.
void say_goodbye() {
    printf("¡Adios, Mundo!\n");
}

int main() {
    // Crea dos botones con funciones diferentes asignadas a su evento onClick.
    Button helloButton = {say_hello, "Decir Hola"};
    Button goodbyeButton = {say_goodbye, "Decir Adios"};

    // Simula hacer clic en los botones.
    button_click(&helloButton);   // Salida: "Boton 'Decir Hola' clickeado. ¡Hola, Mundo!"
    button_click(&goodbyeButton);  // Salida: "Boton 'Decir Adios' clickeado. ¡Adios, Mundo!"

    return 0;
}
```

# Punteros y Estructuras (Structs)

También podemos tener punteros apuntando a estructuras:

C

```
struct Person {
    char name[50];
    int age;
};

struct Person *personPtr; // Como declararias el puntero
```

### Inicialización y acceso (Operador Flecha `->`):

C

```
struct Person personInstance;
personPtr = &personInstance;

// Usamos -> para acceder a los miembros a traves de un puntero
strcpy(personPtr->name, "Alice");
personPtr->age = 30;
```

### Asignación dinámica de memoria con Structs:

C

```
personPtr = (struct Person *) malloc(sizeof(struct Person));

if (personPtr) {
    strcpy(personPtr->name, "Bob");
    personPtr->age = 25;
}

free(personPtr);  // ¡No olvides liberar la memoria!
```

El `(struct Person *)` antes de `malloc` es un **moldeo de tipo** (_type cast_). Le dice explícitamente al compilador que trate el puntero genérico devuelto por `malloc` como un puntero a esa estructura específica.

### Punteros dentro de estructuras (Nodos)

C

```
struct Node {
    int data;
    struct Node *next;
};
```

Aquí, una estructura `Node` contiene un entero y un puntero a otra estructura del mismo tipo `Node`. Esto forma la base estructural de las **listas enlazadas**.

### Punteros a un arreglo de estructuras

C

```
struct Person people[10];
struct Person *arrayPtr;

arrayPtr = people;

(arrayPtr + 2)->age = 28; // Esto establecera la edad de la tercera persona en el arreglo a 28
```

# Punteros Genéricos (`void *`)

Imagina que eres un cartero repartiendo correspondencia. En lugar de conocer los detalles internos de cada casa, lo único que te importa es la dirección en el sobre. De esa manera, puedes entregar correo en cualquier casa, sea grande o pequeña. Un puntero genérico es como ese cartero: no le importa a qué tipo de datos está apuntando, solo guarda una dirección de memoria cruda.

### Declaración

C

```
void *pointerName; // Asi es como se ve
```

### Uso de un puntero genérico

Supongamos que tienes un entero cualquiera y quieres que guarde su dirección:

C

```
int randomNum = 42;          // Solo un numero cualquiera
void *genPtr = &randomNum;   // Nuestro cartero (puntero generico) guardando su direccion
```

Si quieres volver a ver ese número usando el puntero genérico, necesitas decirle al compilador qué tipo de "casa" es mediante un _type cast_:

C

```
int retrievedNum = *(int *)genPtr;   // Dile al compilador: "¡Oye, lo que hay ahi dentro es un entero!"
```

### ¿Por qué usar punteros genéricos?

- **Flexibilidad:** Permiten que el código funcione con cualquier tipo de datos, reduciendo la necesidad de duplicar funciones.
    
- **Agnosticismo de tipos:** Funciones como `malloc()` no necesitan conocer tu tipo de datos, simplemente asignan el tamaño en bytes solicitado y te devuelven un `void *` para que tú lo moldees a tu gusto.
    
- **Emulación de Polimorfismo:** Si quieres simular comportamientos de programación orientada a objetos en C, los punteros genéricos son la herramienta ideal.
    

# Errores comunes con Punteros

## 1. Punteros no inicializados

Si declaras un puntero pero no le asignas una dirección válida, apuntará a un lugar aleatorio de la memoria (un puntero salvaje). Intentar cambiar su valor causará estragos.

C

```
int *ptr;
*ptr = 5;  // ¡ERROR! Desreferenciando un puntero no inicializado
```

**Solución:** Inicialízalos siempre en `NULL` o con una dirección válida.

## 2. Punteros colgantes (Dangling Pointers)

Un puntero colgante ocurre cuando liberas la memoria a la que apunta, pero dejas el puntero existiendo. El puntero sigue apuntando a esa dirección que ya no le pertenece.

C

```
int *ptr = (int *)malloc(sizeof(int));
free(ptr);
*ptr = 4;  // ¡ERROR! ptr es ahora un puntero colgante
```

**Solución:** Después de usar `free()`, iguala inmediatamente el puntero a `NULL` (`ptr = NULL;`). Si intentas usarlo por error, el programa fallará inmediatamente de manera controlada en lugar de corromper datos en silencio.

## 3. Fugas de memoria (Memory Leaks)

Si asignas memoria en el Heap usando `malloc()` y luego pierdes el puntero (por ejemplo, si la función termina o lo reasignas) sin haber usado `free()`, esa memoria se queda bloqueada e inutilizable.

C

```
for(int i = 0; i < 100; i++) {
    int *ptr = (int *)malloc(sizeof(int));
    // Se olvido liberar ptr con free(ptr)
}
```

**Analogía:** Piensa en un estacionamiento público. Si la gente deja sus autos allí y nunca regresa a recogerlos, el estacionamiento eventualmente se quedará sin espacio. El sistema se quedará sin memoria libre y colapsará.

## 4. Desbordamientos de búfer (Buffer Overflows)

Ocurre cuando escribes más datos de los que el bloque asignado puede soportar, invadiendo y sobrescribiendo la memoria vecina.

C

```
char *ptr = (char *)malloc(5 * sizeof(char));  // Asigna espacio para 5 caracteres
strcpy(ptr, "HelloWorld");  // ¡ERROR! Escribe mas alla de la memoria asignada
```

# Resumen Final: ¿Cuándo usar punteros?

- **Asignación dinámica de memoria:** Cuando necesitas definir el tamaño de tus estructuras de datos durante la ejecución y no de forma fija en el código.
    
- **Argumentos de funciones:** Para modificar los valores reales de las variables pasadas a una función (paso por referencia).
    
- **Arreglos y Cadenas:** Para recorrerlos de manera eficiente y pasarlos a funciones sin copiar todos sus datos en la memoria Stack.
    
- **Estructuras de datos complejas:** Para conectar nodos entre sí y crear listas enlazadas, árboles o grafos.
    
- **Punteros a Funciones:** Para lograr un comportamiento dinámico y manejar callbacks o eventos sobre la marcha.