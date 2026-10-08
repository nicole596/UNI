 # Backtracking — Resumen (teoría + código + problemas resueltos)

## 1. ¿Qué es backtracking?

Backtracking es un método sistemático para recorrer **todas** las configuraciones posibles de un espacio de búsqueda. Es un algoritmo general que se personaliza para cada problema específico.

La solución se modela como un vector `a = (a1, a2, ..., an)`, donde cada elemento `ai` se elige de un conjunto finito y ordenado `Si`. Ese vector puede representar, por ejemplo:
- una **permutación** (ai = i-ésimo elemento del orden), o
- un **subconjunto** (ai = verdadero/falso según si el i-ésimo elemento del universo está incluido).

**La idea central:** en cada paso partimos de una solución parcial `a = (a1, ..., ak)` e intentamos extenderla con un elemento más. Después de extenderla, comprobamos si ya es una solución completa. Si no lo es:
- si la solución parcial **puede** extenderse potencialmente → recurrimos y seguimos.
- si **no puede** → quitamos el último elemento (backtrack) e intentamos otra opción para esa posición.

**Backtracking es, en esencia, DFS sobre un grafo implícito de configuraciones.** Garantiza corrección (enumera todas las posibilidades sin repetir), pero para ser *eficiente* hay que **podar (prune)** ramas muertas o redundantes tan pronto como sea posible — esa poda es la que hace posible, por ejemplo, resolver Sudoku a mano.

---

## 2. El template general

```java
void backtrack(int[] a, int k, Data input) {
    int[] c = new int[MAXCANDIDATES];   // candidatos para la siguiente posición
    int[] nc = new int[1];              // cantidad de candidatos

    if (is_a_solution(a, k, input)) {
        process_solution(a, k, input);
    } else {
        k = k + 1;
        construct_candidates(a, k, input, c, nc);
        for (int i = 0; i < nc[0]; i++) {
            a[k] = c[i];
            make_move(a, k, input);
            backtrack(a, k, input);
            unmake_move(a, k, input);
            if (finished) {
                return;   // terminación temprana
            }
        }
    }
}
```

Cuatro piezas que se personalizan por problema:

| Rutina                                     | Rol                                                                                                             |
| ------------------------------------------ | --------------------------------------------------------------------------------------------------------------- |
| `is_a_solution(a, k, input)`               | ¿Los primeros k elementos de `a` forman ya una solución completa?                                               |
| `construct_candidates(a, k, input, c, nc)` | Llena `c` con los candidatos válidos para la posición k, dado lo puesto en 1..k-1. `nc` guarda cuántos son.     |
| `process_solution(a, k, input)`            | Qué hacer con una solución completa (imprimirla, contarla, etc.)                                                |
| `make_move` / `unmake_move`                | (Opcionales) efectos secundarios al colocar/retirar un candidato — útiles para mantener estructuras auxiliares. |

Como `c` se crea de nuevo en cada llamada recursiva, los candidatos "aún no probados" en cada nivel no interfieren entre sí — eso es lo que asegura que no se repita ningún estado.

---

## 3. Problema resuelto #1 — Subconjuntos (Subsets)

**Objetivo:** generar los 2ⁿ subconjuntos de un conjunto de n elementos.

**Modelo:** vector de n celdas booleanas; `ai = true/false` indica si el elemento i está en el subconjunto. `Sk = {true, false}` para toda posición, y `a` es solución cuando `k ≥ n`.

```java
boolean is_a_solution(int[] a, int k, int n) {
    return (k == n);
}

void construct_candidates(int[] a, int k, int n, int[] c, int[] ncandidates) {
    c[0] = 1;              // true
    c[1] = 0;              // false
    ncandidates[0] = 2;    // siempre 2 opciones, sin restricciones
}

void process_solution(int[] a, int k) {
    System.out.print("{ ");
    for (int i = 1; i <= k; i++) {
        if (a[i] == 1) System.out.print(i + " ");
    }
    System.out.println("}");
}
```

`generate_subsets(3)` recorre el árbol binario de profundidad 3 (2³ = 8 hojas/soluciones).

---

## 4. Problema resuelto #2 — Permutaciones

**Objetivo:** generar las n! permutaciones de n elementos.

**Modelo:** `ai ∈ {1..n}` sin repetir. `Sk = {1..n} - a` (los elementos aún no usados), y es solución cuando `k = n`.

```java
void construct_candidates(int[] a, int k, int n, int[] c, int[] ncandidates) {
    boolean[] in_perm = new boolean[NMAX];
    for (int i = 1; i < NMAX; i++) in_perm[i] = false;
    for (int i = 1; i < k; i++) in_perm[a[i]] = true;   // marcar ya usados

    ncandidates[0] = 0;
    for (int i = 1; i <= n; i++) {
        if (!in_perm[i]) {
            c[ncandidates[0]] = i;
            ncandidates[0]++;
        }
    }
}

boolean is_a_solution(int[] a, int k, int n) { return (k == n); }

void process_solution(int[] a, int k) {
    System.out.print("{ ");
    for (int i = 1; i <= k; i++) System.out.print(a[i] + " ");
    System.out.println("}");
}
```

A diferencia de subconjuntos, aquí `construct_candidates` **sí filtra** (excluye los ya usados) — el pruning ya está integrado en la construcción de candidatos.

> **Problema propuesto (del PDF):** un *derangement* es una permutación p de 1..n donde ningún elemento queda en su posición original (`pi ≠ i` para todo i). Se pide un backtracking eficiente con poda que genere todos los derangements — la poda natural es: al construir candidatos para la posición k, excluir tanto los ya usados **como** el valor k mismo.

---

## 5. Problema resuelto #3 — N-Reinas (Eight Queens)

**Objetivo:** colocar 8 reinas en un tablero 8×8 sin que ninguna amenace a otra.

**Representación clave:** como no puede haber dos reinas en la misma columna, una solución completa es una **permutación** de 1..n (cada posición del vector = una columna, el valor = la fila). Esto reduce el espacio de búsqueda de 8⁸ a 8! = 40,320 — manejable.

La rutina crítica es `construct_candidates`: para cada fila candidata `i` en la columna `k`, verifica contra todas las reinas ya colocadas (`j < k`) si hay amenaza de:
- **fila** (`i == a[j]`), o
- **diagonal** (`|k-j| == |i-a[j]|`) — la amenaza de columna queda descartada automáticamente por construcción.

```java
void construct_candidates(int[] a, int k, int n, int[] c, int[] ncandidates) {
    ncandidates[0] = 0;
    for (int i = 1; i <= n; i++) {
        boolean legal_move = true;
        for (int j = 1; j < k; j++) {
            if (Math.abs(k - j) == Math.abs(i - a[j])) legal_move = false; // diagonal
            if (i == a[j]) legal_move = false;                             // fila
        }
        if (legal_move) {
            c[ncandidates[0]] = i;
            ncandidates[0]++;
        }
    }
}

boolean is_a_solution(int[] a, int k, int n) { return (k == n); }

void process_solution(int[] a, int k) {
    solution_count++;   // aquí solo contamos, no imprimimos cada tablero
}

public void solve(int n) {
    int[] a = new int[NMAX];
    this.solution_count = 0;
    this.finished = false;
    backtrack(a, 0, n);
    System.out.printf("n=%d solution_count=%d\n", n, this.solution_count);
}
```

Con esta poda, el programa encuentra las **365,596 soluciones para n=14** en minutos — sin poda sería inviable.

---

## 6. Otros problemas mencionados (sin desarrollo completo en el PDF)

- **Sudoku**: motivación inicial del tema — backtracking + poda de restricciones es lo que permite resolverlo eficientemente.
- **Covering the Chess Board / Little Bishops**: variantes de colocar piezas cumpliendo restricciones de cobertura/amenaza.
- **¿Pueden 8 piezas de ajedrez (rey, reina, 2 torres, 2 alfiles, 2 caballos) amenazar todas las casillas del tablero?** — reto abierto planteado en el material.
- **Prime Ring Problem**: mencionado como tema, sin desarrollo de código en estas diapositivas.

---

## Idea final

En todos los casos el patrón es el mismo: **is_a_solution + construct_candidates + process_solution** son las tres piezas que cambian; `backtrack()` (el DFS implícito con poda) es siempre igual. La eficiencia del algoritmo depende casi enteramente de qué tan agresivamente `construct_candidates` descarta candidatos inválidos antes de recurrir.

Si quieres, puedo generar una simulación interactiva paso a paso (como las que ya tienes de DFS/BFS) para N-Reinas o Subsets/Permutaciones.