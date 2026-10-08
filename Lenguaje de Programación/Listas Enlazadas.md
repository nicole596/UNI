### ¿Qué es?

Una lista enlazada es una estructura de datos lineal donde los elementos no se guardan en ubicaciones de memoria contiguas. En su lugar, cada elemento apunta al siguiente mediante una dirección de memoria, permitiendo que la estructura crezca dinámicamente.

### Nodo

Es la unidad básica de una lista enlazada. Es un bloque de memoria que se divide en dos partes: el dato que queremos guardar (un entero, un texto, etc.) y un puntero (dirección de memoria) que indica dónde está el siguiente nodo.

### Head (Cabeza)

Es un puntero especial que apunta exclusivamente al primer nodo de la lista. Si la lista está completamente vacía, el Head apunta a `NULL`.

### Analogía del tren

Imagina un tren de carga en movimiento. Cada vagón es un **nodo** que lleva un contenedor (el dato) y tiene un enganche físico (el puntero) que lo conecta con el vagón que viene atrás. Si quieres inspeccionar el último vagón, no puedes saltar directamente a él; obligatoriamente tienes que entrar por la locomotora (**Head**) e ir cruzando vagón por vagón hasta llegar al final.

### Características

- **Tamaño dinámico:** A diferencia de los arreglos las listas enlazadas pueden crecer o decrecer sin necesidad de realojar en otro espacio de memoria 
    
- **Inserción y eliminación eficiente:** Agregar o remover elementos solo se necesitan editar unos punteros.
    
- **Acceso secuencial:** Para llegar al elemento n se tiene que atravesar  todos los elementos anteriores desde la cabeza.
    
- **Sobrecosto de memoria:** Cada elemento requiere espacio adicional para guardar el puntero.


### Código
``` C
#include <stdio.h>
#include <stdlib.h>

struct Node {
  int data;
  struct Node* siguiente; //Puntero al nodo siguiente
};

void printList(struct Node* head) {
  struct Node* current = head;
  while (current != NULL) {
    printf("%d -> ", current->data);
    current = current->siguiente; // Avanzar al nodo siguiente
  }
  printf("NULL\n");
}

int main() {
  // asignar espacio de memoria para los nodos
  struct Node* head = (struct Node*)malloc(sizeof(struct Node));
  struct Node* second = (struct Node*)malloc(sizeof(struct Node));

  head->data = 10; 
  head->siguiente = second; // Head now points to the second node

  second->data = 20;
  second->siguiente = NULL; // End of the list

  printList(head);
  
  // Clean up memory
  free(head);
  free(second);
  return 0;
}
```

## Pilas (Stacks - Data Structure)

### ¿Qué es?

Aunque el sistema operativo usa un "Stack" para manejar la memoria automática, una Pila como estructura de datos abstracta funciona igual: es una colección lineal de elementos donde el acceso está restringido a un solo extremo. Se rige estrictamente por el principio **LIFO (Last In, First Out)**.

### Top

Es la posición del último elemento que fue agregado a la pila. Todas las operaciones de lectura, inserción y eliminación ocurren obligatoriamente aquí.

### Analogía de los platos

Imagina una pila de platos limpios en la cocina de un restaurante. Cuando terminas de lavar un plato, lo colocas arriba de todo (**Push**). Cuando un mesero necesita un plato para servir comida, retira el que está arriba de todo (**Pop**). No puedes agarrar el plato del fondo directamente sin el riesgo de destruir toda la estructura.

### Características

- **Last-In, First-Out (LIFO):** El último elemento añadido es el primero en ser quitado.
    
- **Acceso Restringido:** Solo se puede ver o acceder último elemento agregado (se usa la operación `peak`)
    
- **Operaciones de tiempo constante:** Las operaciones push y pop son rápidas pues ningún elemento es realojado.
    
- **Flexibilidad de implementación:** Se puede implementar con un arreglo o una lista dinámica dependiendo de las necesidades

### Código

``` C
#include <stdio.h>
#define MAX 100

struct Stack 
{
  int items[MAX];
  int top;
};

void push(struct Stack* s, int value) 
{
  if (s->top == MAX - 1) return; // Stack Overflow (Full)
  s->top++;
  s->items[s->top] = value;
}

int pop(struct Stack* s) {
  if (s->top == -1) return -1; // Stack Underflow (Empty)
  int value = s->items[s->top];
  s->top--;
  return value;
}

int main() {
  struct Stack s;
  s.top = -1; // Initializing an empty stack

  push(&s, 5);
  push(&s, 15);

  printf("Popped element: %d\n", pop(&s)); // Should print 15 (Last In)
  return 0;
}
```

## Colas (Queues)

### ¿Qué es?

Una Cola es una estructura de datos lineal diseñada para procesar elementos en el orden exacto en que llegaron. Sigue de forma estricta el principio **FIFO (First In, First Out)**.

### Front y Rear

A diferencia de la pila, la cola maneja dos extremos dinámicos: el **Front** (Frente), que apunta al elemento que lleva más tiempo esperando y es el siguiente en salir, y el **Rear** (Final), que apunta al último elemento que se acaba de unir a la estructura.

### Analogía de la fila del supermercado

Piensa en la fila para pagar en el supermercado. La primera persona que llega a la caja es la primera en ser atendida y abandonar la fila (**Front**). Si llega un cliente nuevo con su carrito, tiene que formarse obligatoriamente al final de la fila (**Rear**).

### Características

- **First-In, First-Out (FIFO):** El primer elemento añadido es el primero en salir.
    
- **Two-Point Access:** El ingreso de ocurre al final de la cola, mientras que la salida ocurre en la entrada.
### Código

``` C
#include <stdio.h>
#define MAX 5

struct Queue {
  int items[MAX];
  int front;
  int rear;
};

void enqueue(struct Queue* q, int value) {
  if (q->rear == MAX - 1) return; // Queue is Full
  if (q->front == -1) q->front = 0; // First element initialization
  q->rear++;
  q->items[q->rear] = value;
}

int dequeue(struct Queue* q) {
  if (q->front == -1 || q->front > q->rear) return -1; // Queue is Empty
  int item = q->items[q->front];
  q->front++;
  return item;
}

int main() {
  struct Queue q = {.front = -1, .rear = -1};

  enqueue(&q, 10);
  enqueue(&q, 20);

  printf("Dequeued element: %d\n", dequeue(&q)); // Should print 10 (First In)
  return 0;
}
```

## Árboles (Trees)

### ¿Qué es?

Un árbol es una estructura de datos **no lineal** y jerárquica. En lugar de conectar elementos en una secuencia plana de izquierda a derecha, los organiza en niveles ramificados, simulando una estructura de árbol invertido.

### Componentes de un Árbol

- **Raíz (Root):** El nodo superior único del que desciende todo el árbol. No tiene ningún nodo padre.
    
- **Padre / Hijo (Parent / Child):** Un nodo es "padre" si se conecta directamente con nodos de un nivel inferior, los cuales se convierten en sus "hijos".
    
- **Hoja (Leaf):** Nodos terminales ubicados en los extremos del árbol que no tienen ningún hijo.
    

### Analogía del sistema de carpetas

Piensa en el almacenamiento de tu computadora. Tienes un disco principal llamado `C:` o `Mero_Disco` (**Raíz**). Dentro de él creas las carpetas `Documentos` e `Imágenes` (**Hijos**). Y dentro de `Documentos` tienes un archivo final llamado `resumen.txt` (**Hoja**). Es una jerarquía donde todo está conectado pero ramificado.

### Características

- **Hierarchical Organization:** Represents data that naturally has a master-subordinate or nested relationship rather than a linear sequence.
    
- **Non-Linear Paths:** Unlike lists, there are multiple branching paths from the root down to the leaves.
    
- **Efficient Searching:** In specialized trees like Binary Search Trees (BST), searching for data is extremely fast, operating in logarithmic time ($O(\log n)$).
    
- **Recursive Nature:** Every single child node can be treated as the root of its own independent "sub-tree," meaning most tree algorithms rely on recursion.

### Código


``` C
#include <stdio.h>
#include <stdlib.h>

struct TreeNode {
  int data;
  struct TreeNode* left;  // Pointer to the left child node
  struct TreeNode* right; // Pointer to the right child node
};

struct TreeNode* createNode(int value) {
  struct TreeNode* newNode = (struct TreeNode*)malloc(sizeof(struct TreeNode));
  newNode->data = value;
  newNode->left = NULL;
  newNode->right = NULL;
  return newNode;
}

// Simple In-Order traversal (Left, Root, Right)
void printTree(struct TreeNode* root) {
  if (root == NULL) return;
  printTree(root->left);
  printf("%d ", root->data);
  printTree(root->right);
}

int main() {
  // Creating a small hierarchical binary tree structure
  struct TreeNode* root = createNode(1);
  root->left = createNode(2);
  root->right = createNode(3);

  printf("Tree In-Order traversal: ");
  printTree(root); // Outputs elements based on structure hierarchy
  printf("\n");

  // Clean up memory from the heap
  free(root->left);
  free(root->right);
  free(root);
  return 0;
}
```