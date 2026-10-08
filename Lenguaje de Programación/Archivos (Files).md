## ¿Qué es?

Un archivo es una colección de bytes almacenada en un dispositivo de almacenamiento secundario permanente (como un disco duro o SSD). Mientras que las variables del programa desaparecen del _Stack_ o del _Heap_ al cerrar la aplicación, los archivos permiten lograr la **persistencia de los datos**, es decir, guardar información para poder leerla o modificarla en el futuro.

## Puntero a Archivo (`FILE*`)

Es un puntero especial definido en la librería `<stdio.h>`. No apunta a un dato común, sino a una estructura interna del sistema operativo que contiene toda la información de control sobre el archivo: su ubicación física, el tamaño, la posición actual de lectura/escritura y el estado de sus permisos.

## Modos de Apertura

Al abrir un archivo, se debe especificar obligatoriamente un "modo" para indicarle al sistema qué pretendemos hacer con él:

- **`"r"` (Lectura / Read):** Abre un archivo existente para leerlo. Si el archivo no existe, produce un error.
    
- **`"w"` (Escritura / Write):** Crea un archivo vacío para escribir en él. Si el archivo ya existía, **borra todo su contenido** para dejarlo en blanco.
    
- **`"a"` (Añadir / Append):** Abre un archivo para escribir al final de este. No borra los datos existentes, sino que "engancha" la nueva información al último byte.

## Analogía del Archivador de Oficina

Imagina la memoria RAM como tu escritorio de trabajo: es rápido, pero al final del día limpias todo y lo que no guardaste se pierde. Un archivo es una **carpeta de cartón** guardada dentro de un **archivador de metal** (el disco duro).

El puntero `FILE*` es tu **asistente de oficina**. Tú no vas directamente al archivador; le pides a tu asistente que busque la carpeta (`fopen`), él la abre en tu escritorio y mantiene su dedo señalando la línea donde vas leyendo o escribiendo. Al terminar, debes ordenarle que cierre la carpeta (`fclose`) y la regrese al mueble para que no se arruine.

## Características

- **Persistencia de Datos:** Permite que la información sobreviva aun si la computadora se apaga o el programa se cierra.
    
- **Flujo Secuencial (Buffer):** C no lee el disco duro byte por byte directamente porque sería muy lento. Utiliza un "buffer" (un área de tránsito en la RAM) para leer y escribir bloques grandes de datos de golpe.
    
- **Manejo de Errores Obligatorio:** Las operaciones con archivos pueden fallar fácilmente (por falta de permisos, disco lleno o archivo inexistente), por lo que siempre se debe verificar si el puntero es igual a `NULL` antes de usarlo.
    
- **Tipos de Formato:** Se pueden manipular como archivos de **Texto** (legibles por humanos, como un `.txt`) o archivos **Binarios** (datos crudos optimizados para la computadora, como un `.dat` o una imagen).

## Código

``` C
#include <stdio.h>

int main() {
  // 1. Declarar el puntero al archivo
  FILE* archivo;

  // 2. Abrir el archivo en modo Escritura ("w")
  archivo = fopen("datos.txt", "w");

  // Control de errores: Verificar si el sistema permitió abrir el archivo
  if (archivo == NULL) {
    printf("Error: No se pudo crear o abrir el archivo.\n");
    return 1; 
  }

  // 3. Escribir información dentro del archivo usando fprintf
  fprintf(archivo, "Línea 1: Guardando texto persistente.\n");
  fprintf(archivo, "Línea 2: El año actual es 2026.\n");

  // 4. Cerrar el archivo de forma obligatoria para asegurar que los datos se guarden
  fclose(archivo);
  printf("Archivo guardado y cerrado con éxito.\n");

  // --- AHORA VAMOS A LEER EL ARCHIVO CREADO ---
  
  char linea[100];
  archivo = fopen("datos.txt", "r"); // Reabrir en modo Lectura ("r")

  if (archivo != NULL) {
    printf("\n--- Contenido leído desde el archivo ---\n");
    // Leer línea por línea hasta llegar al final del archivo (EOF)
    while (fgets(linea, sizeof(linea), archivo) != NULL) {
      printf("%s", linea);
    }
    fclose(archivo); // Cerrar después de leer
  }

  return 0;
}
```