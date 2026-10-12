# Fundamentos

## 1. TAD Grafo: conceptos básicos

Un grafo `G = (V, A)` es un par formado por un conjunto de **vértices** `V` y un conjunto de **aristas** `A`. `|V|` = número de vértices, `|A|` = número de aristas.

**Clasificaciones clave:**
- **Dirigido vs. No dirigido**: en un grafo no dirigido, `{x,y} ∈ A` implica `{y,x} ∈ A` (la relación es simétrica). Redes de carreteras suelen ser no dirigidas; redes de calles con sentido único son dirigidas.
- **Ponderado vs. no ponderado**: en un grafo ponderado, cada arista (o vértice) tiene un costo numérico asociado.
- **Simple vs. no simple**: un grafo simple no tiene *self-loops* (arista de un vértice a sí mismo) ni *multi-edges* (arista repetida). En este curso solo se trabaja con grafos simples.
- **Denso vs. disperso (sparse)**: denso cuando `|A|` se acerca al máximo posible (`Θ(n²)`); disperso cuando `|A|` crece linealmente con `n`. Esta distinción determina qué estructura de datos conviene usar.

Cotas de `|A|`:
- Dirigido simple: `0 ≤ |A| ≤ n·(n-1)`
- No dirigido simple: `0 ≤ |A| ≤ n·(n-1)/2`

Un **camino** es una secuencia de vértices donde existe una arista entre cada uno y el siguiente. Un **camino simple** no repite vértices.

---

## 2. Matriz de Adyacencia vs. Lista de Adyacencia

### Matriz de Adyacencia

Matriz `M` de `n × n` donde `M[i][j] = 1` si `(i,j)` es arista, `0` en caso contrario.

```
  if (i,j) es una arista
		Mij = 1,
  0, en otro caso
```

- En grafos **no dirigidos**, la matriz es **simétrica**: `Mij = Mji`.
- En grafos **dirigidos**, generalmente **no** es simétrica.
- En grafos **ponderados**, en vez de 1/0 se guarda el peso, y `∞` donde no hay arista.

**Costos:** espacio `O(n²)` sin importar cuántas aristas haya realmente. Verificar si `(i,j)` es arista cuesta `O(1)` (acceso directo). Recorrer todos los vecinos de un vértice cuesta `O(n)` aunque tenga pocos vecinos → **excesivo cuando el grafo es disperso**.

### Lista de Adyacencia

Un arreglo de `n` punteros, donde el elemento `i` apunta a una lista de los vértices adyacentes a `i`.

- Probar si `(i,j) ∈ A` cuesta `O(dᵢ)`, donde `dᵢ` es el *degree* (grado) de `i` — puede ser mucho menor que `n` en grafos dispersos.
- Espacio proporcional a `|V| + |A|`, mucho más eficiente que la matriz cuando el grafo es disperso.

**List in Array Representation** (la que usa este curso): en vez de listas enlazadas, las aristas se guardan en un arreglo `MAXV × MAXDEGREE`.

```java
public class Graph {
    private static final int MAXV = 100;       // máximo número de vértices
    private static final int MAXDEGREE = 50;    // máximo grado de salida
    private int[][] edges;      // información de adyacencia
    private int[] degree;       // grado de salida de cada vértice
    public int nvertices;       // número de vértices
    private int nedges;         // número de aristas
    private boolean isDirected;

    // Atributos de estado para BFS/DFS
    public boolean[] processed;
    public boolean[] discovered;
    public int[] parent;
}
```

**Inserción de una arista** (nótese la recursión para manejar el caso no dirigido):

```java
public void insertEdge(int x, int y, boolean directed) {
    this.edges[x][this.degree[x]] = y;
    this.degree[x]++;
    this.nedges++;
    if (!directed) {
        insertEdge(y, x, true);  // agrega la arista inversa
    }
}
```

> **Importante:** en un grafo no dirigido, cada arista se almacena **dos veces** (una en cada extremo) → `nedges` cuenta aristas únicas, pero `degree` suma ambas copias.

### Trade-off

| | Matriz | Lista |
|---|---|---|
| Espacio | `O(n²)` | `O(n + m)` |
| ¿(i,j) es arista? | `O(1)` | `O(degree(i))` |
| Recorrer vecinos de i | `O(n)` | `O(degree(i))` |
| Mejor para | grafos densos | grafos dispersos (caso más común) |

Ambas representaciones son útiles, pero **las listas de adyacencia suelen ser mejores para la mayoría de problemas** — es la que se usa en las implementaciones de BFS/DFS de este curso.

---

## 3. BFS — Breadth-First Search

BFS es apropiado cuando interesan los **caminos más cortos** (shortest paths) en grafos **no ponderados**. Explora el grafo por **niveles**: primero todos los vecinos directos, luego los vecinos de los vecinos, etc.

**Estados de un vértice:** `undiscovered → discovered → processed`
- **discovered**: la primera vez que se visita.
- **processed**: después de haber recorrido todas sus aristas salientes.

BFS usa una **cola (Queue, FIFO)**: los vértices más antiguos en la cola se procesan primero — que son exactamente los más cercanos a la raíz.

```java
public void bfs(int start) {
    Queue<Integer> q = new LinkedList<>();
    int v;
    q.add(start);
    this.discovered[start] = true;
    while (!q.isEmpty()) {
        v = q.poll();
        this.processVertex(v);
        this.processed[v] = true;
        for (int i = 0; i < this.degree[v]; i++) {
            int nextVertex = this.edges[v][i];
            if (this.validEdge(nextVertex)) {
                if (!this.discovered[nextVertex]) {
                    q.add(nextVertex);
                    this.discovered[nextVertex] = true;
                    this.parent[nextVertex] = v;
                }
                if (!this.processed[nextVertex]) {
                    this.processEdge(v, nextVertex);
                }
            }
        }
    }
}
```

**Propiedad clave:** en BFS, los vértices se descubren en orden de **distancia creciente** desde la raíz. El camino único en el árbol BFS desde la raíz hasta cualquier nodo `x` usa el **mínimo número de aristas posible**.

**Reconstrucción de caminos (`findPath`)**: como `parent[]` solo permite subir de hijo a padre, para imprimir el camino en el orden correcto (raíz → destino) se usa recursión, que invierte el orden automáticamente:

```java
public void findPath(int start, int end) {
    if ((start == end) || (end == -1)) {
        System.out.print("\n" + start);
    } else {
        findPath(start, this.parent[end]);   // primero sube al padre
        System.out.print(" " + end);          // imprime AL REGRESAR
    }
}
```

---

## 4. DFS — Depth-First Search

DFS usa la misma idea que **backtracking**: avanza tanto como sea posible y retrocede cuando ya no hay posibilidades sin explorar. Puede pensarse como **BFS con una pila (Stack) en lugar de una cola** — explora en profundidad antes que en anchura.

### Versión recursiva (la pila de llamadas de Java hace el trabajo implícitamente)

```java
public void dfs(int v) {
    if (this.finished) return;      // permite terminación temprana
    this.discovered[v] = true;
    this.processVertex(v);
    for (int i = 0; i < this.degree[v]; i++) {
        int nextVertex = this.edges[v][i];
        if (this.validEdge(nextVertex)) {
            if (!this.discovered[nextVertex]) {
                this.parent[nextVertex] = v;
                this.dfs(nextVertex);
            } else if ((!this.processed[nextVertex] && this.parent[v] != nextVertex) || this.isDirected) {
                this.processEdge(v, nextVertex);
            }
        }
        if (this.finished) return;
    }
    this.processed[v] = true;   // se marca AL SALIR (post-order)
}
```

### Versión iterativa (pila explícita)

```java
public void dfsIterativo(int start) {
    Deque<Integer> q = new ArrayDeque<>();
    q.push(start);
    this.discovered[start] = true;
    while (!q.isEmpty()) {
        int v = q.pop();
        this.processVertex(v);
        this.processed[v] = true;
        // vecinos en orden inverso para acercar el orden al DFS recursivo
        for (int i = this.degree[v] - 1; i >= 0; i--) {
            int nextVertex = this.edges[v][i];
            if (this.validEdge(nextVertex)) {
                if (!this.discovered[nextVertex]) {
                    q.push(nextVertex);
                    this.discovered[nextVertex] = true;
                    this.parent[nextVertex] = v;
                }
                if (!this.processed[nextVertex]) {
                    this.processEdge(v, nextVertex);
                }
            }
        }
    }
}
```

### BFS vs DFS — diferencia central

| | BFS | DFS |
|---|---|---|
| Estructura | Queue (FIFO) | Stack (LIFO) — explícita o call stack |
| Orden de exploración | por niveles | en profundidad |
| `processed[v]=true` | inmediato al desencolar | al retornar (post-order) — solo DFS recursivo |
| Útil para | shortest paths (grafo no ponderado) | backtracking, ciclos, orden topológico |

El **mismo algoritmo**, cambiando solo `push/pop` por `add/poll`, pasa de DFS a BFS — esa es la elegancia de la estructura auxiliar.

---

## 5. Componentes Conectados

Los **connected components** de un grafo no dirigido son las "piezas" separadas tales que no hay conexión entre piezas. Todo lo que se descubre en un BFS (o DFS) desde un vértice pertenece al **mismo** componente conexo.

**Algoritmo:** repetir BFS/DFS desde cualquier vértice aún `undiscovered`, incrementando un contador de componente cada vez que se necesita un nuevo punto de partida.

```java
public void connectedComponents() {
    int c = 0;   // número de componente
    this.initializeSearch();
    for (int i = 1; i <= this.nvertices; i++) {
        if (!this.discovered[i]) {
            c++;
            System.out.printf("Component %d:", c);
            this.bfs(i);
            System.out.println();
        }
    }
}
```

Con `processVertex` personalizado para simplemente imprimir el vértice (`processEdge` vacío), cada llamada a `bfs(i)` imprime todos los vértices de un componente.

**Aplicación clásica:** decidir si un puzzle (como el Cubo de Rubik o el 15-puzzle) es resoluble desde cualquier posición inicial equivale a preguntar si el grafo de configuraciones legales es **conexo** (un solo componente).

**Ejemplo con 3 componentes:**
```java
Graph g = new Graph(false);
g.nvertices = 7;
// Componente 1: 1-2, 1-3
g.insertEdge(1, 2, false);
g.insertEdge(1, 3, false);
// Componente 2: 4-5
g.insertEdge(4, 5, false);
// Componente 3: 6-7
g.insertEdge(6, 7, false);
g.connectedComponents();
```

---

## Idea final

`initializeSearch()`, `processVertex()` y `processEdge()` son el "molde" común: BFS y DFS son el **mismo esqueleto de recorrido**, y lo que cambia es (a) la estructura auxiliar (cola vs pila) y (b) qué hacen `processVertex`/`processEdge` en cada aplicación — desde simplemente imprimir vértices, hasta detectar bipartición, componentes conexos, ciclos, o construir el árbol de expansión mínima más adelante.

Como ya tienes varias simulaciones interactivas de BFS/DFS/componentes en tu proyecto (`bfs_grafo10aristas.html`, `dfs_iterativo_explicacion.html`, `dfs_recursivo_explicacion.html`), si quieres puedo armar una similar específica para **componentes conectados**, mostrando cómo se van descubriendo las distintas "piezas" del grafo paso a paso.