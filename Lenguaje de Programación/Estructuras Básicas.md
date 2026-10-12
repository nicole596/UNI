## Estructuras (struct)

### ¿Qué es?

Una estructura (`struct`) es un tipo de dato compuesto que permite agrupar múltiples variables de diferentes tipos bajo un mismo nombre. A diferencia de un arreglo (donde todos los elementos deben ser del mismo tipo), una estructura une datos que están relacionados lógicamente pero que tienen naturalezas distintas.

### Miembros

Se les llama "miembros" o "campos" a cada una de las variables individuales que viven dentro de la estructura. Cada miembro tiene su propio nombre y su propio tipo de dato.

### Analogía de la Ficha Técnica

Imagina la ficha de registro de un automóvil en una base de datos. Para describir el carro no te basta con un solo número. Necesitas texto para la `marca`, un entero para el `año` y un número decimal para el `precio`. La estructura es la "plantilla" o el formulario vacío, y cada carro que registras es una instancia independiente con sus propios datos específicos.

### Características

- **Datos Heterogéneos:** Puede almacenar múltiples tipos de datos diferentes (enteros, caracteres, punteros u otras estructuras) en un solo bloque.
    
- **Memoria Contigua:** Los miembros se asignan de forma secuencial en la memoria, aunque el compilador puede insertar bytes vacíos (_padding_) para la alineación del procesador.
    
- **Memoria Independiente:** Cada miembro tiene su propia dirección de memoria dedicada. Modificar un miembro no afecta en absoluto a los demás.
    
- **Copia por Valor:** Cuando se pasa una estructura a una función sin usar punteros, C saca una copia completa de toda la estructura, lo que puede generar un alto consumo de memoria si la estructura es muy grande.
    

### Código

``` C
#include <stdio.h>
#include <string.h>

// Definiendo la plantilla de la estructura
struct Carro {
  char marca[20];
  int anio;
  float precio;
};

int main() {
  // Creando una instancia de la estructura
  struct Carro miCarro;

  // Asignando valores a los miembros usando el operador punto (.)
  strcpy(miCarro.marca, "Toyota");
  miCarro.anio = 2025;
  miCarro.precio = 25500.50;

  printf("Carro: %s, Año: %d, Precio: $%.2f\n", miCarro.marca, miCarro.anio, miCarro.precio);
  return 0;
}
```

## Enumeraciones (enum)

### ¿Qué es?

Un `enum` (enumeración) es un tipo de dato definido por el usuario que se utiliza para asignar nombres legibles a un conjunto de constantes enteras. Sirve para evitar el uso de "números mágicos" en el código, reemplazándolos con palabras descriptivas que hacen que el programa sea mucho más fácil de leer y mantener.

### Elementos (Enumeradores)

Son las etiquetas o palabras clave que defines dentro del enum. Por defecto, C le asigna un número entero automático a cada una, empezando desde el `0` para la primera, `1` para la segunda, y así sucesivamente.

### Analogía del Semáforo

Imagina el estado de un semáforo. Solo puede estar en tres estados posibles: Verde, Amarillo o Rojo. En la mente de la computadora, estos estados se manejan internamente como números ($0, 1, 2$), pero para un programador humano es mucho más fácil y seguro leer la palabra `VERDE` en una condición que intentar recordar qué significaba el número $0$.

### Características

- **Legibilidad del Código:** Reemplaza constantes numéricas oscuras por palabras significativas y fáciles de entender para los humanos.
    
- **Seguridad de Tipos (Básica):** Ayuda a restringir una variable para que solo pueda tomar un conjunto de valores válidos previamente definidos.
    
- **Enteros Subyacentes:** Por debajo, los enums son tratados simplemente como enteros estándar (`int`). Puedes cambiar sus valores por defecto manualmente al definirlos (por ejemplo: `ESTADO = 4`).
    
- **Optimización en Switch-Case:** Es altamente eficiente cuando se combina con estructuras `switch` para crear máquinas de estado o selectores de menú.
    

### Código

``` C
#include <stdio.h>

// Definiendo el enum
enum EstadoSemaforo {
  VERDE,    // Internamente vale 0
  AMARILLO, // Internally vale 1
  ROJO      // Internamente vale 2
};

int main() {
  // Creando una variable de tipo enum
  enum EstadoSemaforo luzActual = ROJO;

  // Usando el enum en una estructura condicional
  if (luzActual == ROJO) {
    printf("¡Alto! El semáforo está en ROJO (%d).\n", luzActual);
  }
  
  return 0;
}
```

## Uniones (union)

### ¿Qué es?

Una unión (`union`) es un tipo de dato compuesto que, a nivel de escritura, se ve idéntica a una estructura, pero funciona de forma completamente opuesta en la memoria. Una unión permite almacenar diferentes tipos de datos en la **misma ubicación exacta de memoria**.

### Compartición de Memoria

A diferencia de un `struct` donde cada miembro tiene su propio espacio, en un `union` todos los miembros comparten el mismo espacio físico. Esto significa que **solo puedes guardar un valor a la vez**. Si escribes un dato en un miembro, se borrará o corromperá lo que estaba en los otros.

### Analogía del Dormitorio con una Sola Cama

Imagina una habitación de hotel que solo tiene una cama individual. En esa habitación pueden hospedarse un Ingeniero, un Doctor o un Artista, pero **no los tres al mismo tiempo**. Si el Doctor entra y se acuesta en la cama (guardas un dato tipo `float`), el Ingeniero que estaba antes tiene que levantarse e irse (el dato tipo `int` se destruye). El tamaño de la habitación (la memoria total asignada) se define por el huésped más grande.

### Características

- **Asignación de Memoria Compartida:** Todos los miembros de la unión comienzan exactamente en la misma dirección de memoria.
    
- **Exclusión Mutua:** Solo un miembro puede contener un valor válido en un momento dado. Escribir en un nuevo miembro sobrescribe los datos del anterior.
    
- **Cálculo del Tamaño:** El tamaño total en bytes de una unión está determinado por el tamaño de su miembro más grande, no por la suma de todos ellos.
    
- **Máxima Eficiencia de Espacio:** Es muy utilizada en programación de bajo nivel, sistemas embebidos o comunicación con registros de hardware donde la memoria es extremadamente limitada.
    

### Código

C

``` C
#include <stdio.h>

// Definiendo la unión
union DatoCompartido {
  int entero;
  float decimal;
  char caracter;
};

int main() {
  union DatoCompartido miDato;

  // El tamaño lo determina el tipo más grande (int y float suelen medir 4 bytes)
  printf("Tamaño total en memoria de la unión: %lu bytes\n", sizeof(miDato));

  miDato.entero = 105;
  printf("Dato como entero: %d\n", miDato.entero);

  // Sobrescribiendo el mismo espacio de memoria con un float
  miDato.decimal = 99.45;
  printf("Dato como decimal: %.2f\n", miDato.decimal);

  // CRÍTICO: Si imprimes el entero ahora, verás basura porque fue sobrescrito
  printf("Dato antiguo entero (corrupto): %d\n", miDato.entero);

  return 0;
}
```