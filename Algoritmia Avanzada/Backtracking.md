# Introducción

Es un método para encontrar todas las posibles soluciones en un espacio de búsqueda mediante la iteración (Deep First Search).

En un vector solución parcial $a = ( a_1,  a_2,  \dots, a_n)$ donde cada $a_1 \in S_1$ , agregamos otro elemento para extenderla. Luego probamos si lo que tenemos es una solución o no:

- Si **sí**, recurrimos y continuamos.
- Si **no**, eliminamos el ultimo elemento de $a$ e intentamos otra posibilidad para esa posición si es que existe.

Para una **permutación** $a_1 =$ i-ésimo elemento del orden. Para un **subconjunto** $a_1 =$ verdadero o falso si el elemento pertenece o no al conjunto.
### Pseudocódigo

``` 
Backtrack (a, k)
if a is a solution; print(a)
else{
	k = k + 1
	compute S_k
	while S_k != 0 do
		a_k = an element in S_k
		Backtrack (a, k)
}
```

# Código

## Implementación

``` Java
void backtrack(int[] a, int k, Data input) {
	int[] c = new int[MAXCANDIDATES]; // candidatos para la siguiente posición
	int[] nc = new int[1]; // cantidad de candidatos (simulamos puntero)
	
	if (is_a_solution(a, k, input)) {
		process_solution(a, k, input);
	} 
	
	else {
		k = k + 1;
		construct_candidates(a, k, input, c, nc);
		for (int i = 0; i < nc[0]; i++) {
			a[k] = c[i];
			make_move(a, k, input);
			backtrack(a, k, input);
			unmake_move(a, k, input);
			if (finished) {
			return; // terminar temprano
		}
	}
}
```

| Rutina                                     | Rol                                                                                                             |
| ------------------------------------------ | --------------------------------------------------------------------------------------------------------------- |
| `is_a_solution(a, k, input)`               | ¿Los primeros k elementos de `a` forman ya una solución completa?                                               |
| `construct_candidates(a, k, input, c, nc)` | Llena `c` con los candidatos válidos para la posición k, dado lo puesto en 1..k-1. `nc` guarda cuántos son.     |
| `process_solution(a, k, input)`            | Qué hacer con una solución completa (imprimirla, contarla, etc.)                                                |
| `make_move` / `unmake_move`                | (Opcionales) efectos secundarios al colocar/retirar un candidato — útiles para mantener estructuras auxiliares. |
## Plantilla

``` Java
public class BacktrackingFramework {
static final int MAXCANDIDATES = 100;
static boolean finished = false;
/**
* Método principal de backtracking
* @param a vector solución
* @param k posición actual (índice del último elemento añadido)
* @param input datos de entrada del problema específico
*/
void backtrack(int[] a, int k, Data input) {
	int[] c = new int[MAXCANDIDATES]; // candidatos para la siguiente posición
	int[] nc = new int[1]; // cantidad de candidatos (simulamos puntero)
	if (is_a_solution(a, k, input)) {
		process_solution(a, k, input);
	} 
	else {
		k = k + 1;
		construct_candidates(a, k, input, c, nc);
		for (int i = 0; i < nc[0]; i++) {
			a[k] = c[i];
			make_move(a, k, input);
			backtrack(a, k, input);
			unmake_move(a, k, input);
			if (finished) {
				return; // terminar temprano
			}
		}
}

// Determina si los primeros k elementos de a forman una solución completa

static boolean is_a_solution(int[] a, int k, Data input) {
// Implementar según el problema específico
return false;
}

/**
* Construye el arreglo de candidatos para la posición k
* @param c arreglo donde se almacenan los candidatos
* @param nc arreglo de un elemento que contiene la cantidad de candidatos
*/

static void construct_candidates(int[] a, int k, Data input, int[] c, int[] nc) {
// Implementar según el problema específico
nc[0] = 0;
}

/**
* Procesa una solución completa (imprime, cuenta, etc.)
*/

static void process_solution(int[] a, int k, Data input) {
// Implementar según el problema específico
}

/**
* Realiza acciones al hacer un movimiento (opcional)
*/

static void make_move(int[] a, int k, Data input) {
// Implementar si es necesario para el problema
}

/**
* Deshace las acciones al retroceder (opcional)
*/

static void unmake_move(int[] a, int k, Data input) {
// Implementar si es necesario para el problema
}

class Data{
}
```

# Subsets

Para construir $2^n$ conjuntos de datos se crea un arreglo de $n$ con verdadero o falso para $a_1$.

El vector de $n$ celdas booleanas; `ai = true/false` indica si el elemento i está en el subconjunto. `Sk = {true, false}` para toda posición, y `a` es solución cuando `k ≥ n`.

## Código

``` Java
public class Subsets {
	static final int NMAX = 8; // Número maximo de elementos
	static final int MAXCANDIDATES = 2; // Solo dos opciones: estar o no estar
	private boolean finished = false;
	void backtrack(int[] a, int k, int n) {
		 int[] c = new int[MAXCANDIDATES];
		 int[] ncandidates = new int[1]; // WRAPPER
		 int i;
		 if (is_a_solution(a, k, n)) {
			 process_solution(a, k);
		 } 
		 else {
			 k++;
			 construct_candidates(a, k, n, c, ncandidates);
			 for (i = 0; i < ncandidates[0]; i++) {
				 a[k] = c[i];
				 backtrack(a, k, n);
				 if (finished) return;
			 }
		 }
	}

 
	boolean is_a_solution(int[] a, int k, int n) {
	 return (k == n);
	 }
	 
	 void construct_candidates(int[] a, int k, int n, int[] c, int[] ncandidates) {
		 // usando int: 1 = true, 0 = false.
		 c[0] = 1;
		 c[1] = 0;
		 ncandidates[0] = 2;
	 }
	 
	void process_solution(int[] a, int k) {
		System.out.print("{ ");
		for (int i = 1; i <= k; i++) {
		 // Si a[i] es 1 (true), entonces el elemento i es parte del subconjunto
			 if (a[i] == 1) {
				 System.out.print(i+ " ");
			 }
		}
		System.out.println("}");
	}
	
	public void generate_subsets(int n) {
		int[] a = new int[NMAX];
		this.finished = false;
		backtrack(a, 0, n);
	}
}

public static void main(String[] args) {
	Subsets subsetsGenerator = new Subsets();
	subsetsGenerator.generate_subsets(3);
}
```

`generate_subsets(3)` recorre el árbol binario de profundidad 3 (2³ = 8 hojas/soluciones).

# Permutaciones

Genera las $n!$ permutaciones para $n$ elementos. Donde `ai ∈ {1..n}` sin repetir. `Sk = {1..n} - a` (los elementos aún no usados), y es solución cuando `k = n`.

```  Java
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

# Problemas

##   1. N-Reinas

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

