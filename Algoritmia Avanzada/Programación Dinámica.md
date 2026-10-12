# 1. ¿Qué es Programación Dinámica (DP)?

DP es una herramienta poderosa y general para resolver **problemas de optimización sobre ítems ordenados** (cadenas de caracteres, secuencias, etc.). El algoritmo de Floyd (all-pairs shortest path) es un ejemplo clásico de DP.

### Greedy vs. Exhaustive Search vs. DP:

- **Greedy**: toma la mejor decisión local en cada paso. Sin una prueba de corrección, tiene muchas probabilidades de fallar.
- **DP**: busca sistemáticamente *todas* las posibilidades (garantiza corrección, como la búsqueda exhaustiva) pero **guarda resultados parciales** para no recalcularlos (aporta eficiencia).

**Recurrence relations:** una ecuación definida en términos de sí misma. Muchas funciones naturales se expresan así:

| Tipo        | Recurrencia             | Forma cerrada |
| ----------- | ----------------------- | ------------- |
| Polinomio   | `an = an-1 + 1`, `a1=1` | `an = n`      |
| Exponencial | `an = 2·an-1`, `a1=2`   | `an = 2ⁿ`     |
| "Rara"      | `an = n·an-1`, `a1=1`   | `an = n!`     |

Los programas pueden evaluar una recurrencia incluso si no tiene forma cerrada bonita — ahí es donde entra DP.

---

## Números de Fibonacci

`Fn = Fn-1 + Fn-2`, con `F0=0, F1=1`.

### Versión recursiva ingenua (lenta)

```java
long fib_r(int n) {
    if (n == 0) return 0;
    if (n == 1) return 1;
    return fib_r(n - 1) + fib_r(n - 2);
}
```

**¿Qué tan lenta?** El árbol de recursión recalcula los mismos subproblemas una y otra vez. Calcular `Fn` requiere aproximadamente **1.6ⁿ** llamadas — crece explosivamente (1.6 ≈ φ = razón áurea ≈ 1.61803, ya que `Fn+1/Fn → φ`).

### Versión con memoización (top-down, cacheando)

```java
static final int MAXN = 45;
static final int UNKNOWN = -1;
private long[] f = new long[MAXN + 1];

long fib_c(int n) {
    if (f[n] == UNKNOWN) {
        f[n] = fib_c(n - 1) + fib_c(n - 2);
    }
    return f[n];
}

long fib_c_driver(int n) {
    f[0] = 0;
    f[1] = 1;
    for (int i = 2; i <= n; i++) {
        f[i] = UNKNOWN;
    }
    return fib_c(n);
}
```

Cachea cada llamada la primera vez que se calcula — evita recomputación, pero sigue siendo recursivo.

### Versión Dynamic Programming (bottom-up)

```java
long fib_dp(int n) {
    long[] f_local = new long[MAXN + 1];
    f_local[0] = 0;
    f_local[1] = 1;
    for (int i = 2; i <= n; i++) {
        f_local[i] = f_local[i - 1] + f_local[i - 2];
    }
    return f_local[n];
}
```

Calcula `Fn` en **tiempo lineal**, construyendo la tabla de abajo hacia arriba en lugar de recursar. **Moraleja: cambiamos espacio por tiempo.**

**Aplicaciones prácticas de DP mencionadas:** morphing en gráficos por computadora, compresión de datos para códigos de barras de alta densidad, diseño de genes para evitar/contener patrones específicos.

---

## Coeficientes Binomiales

**El truco general de DP:** un algoritmo recursivo ingenuo recalcula los mismos subproblemas repetidamente; guardar las respuestas en una tabla (en vez de recomputar) da un algoritmo eficiente. Metodología: **primero** encontrar un algoritmo recursivo correcto, **luego** acelerarlo con una matriz de resultados.

`C(n,k)` cuenta las formas de elegir k cosas de n posibilidades. Dos interpretaciones útiles:
- **Comités**: formas de armar un comité de k miembros de n personas → `C(n,k)`.
- **Caminos en una grilla**: formas de ir de la esquina superior-izquierda a la inferior-derecha de una grilla n×m moviéndose solo "abajo" y "derecha". Cada camino tiene n+m pasos → hay `C(n+m, n)` caminos.

**Por qué no calcular con factoriales directamente:** aunque `C(n,k) = n! / ((n-k)!·k!)`, los cálculos intermedios (factoriales grandes) pueden causar **overflow aritmético** incluso cuando el resultado final cabe perfectamente en un entero.

### Recurrencia de Pascal (más estable)

El Triángulo de Pascal: cada número es la suma de los dos números directamente encima. Esto da la recurrencia:

```
C(n, k) = C(n-1, k-1) + C(n-1, k)
```

Funciona porque el n-ésimo elemento **o aparece o no aparece** en cada subconjunto de tamaño k — se particiona el conteo en esos dos casos.

**Casos base:**
- `C(n, 0) = 1` — solo hay una forma de elegir 0 cosas (el conjunto vacío).
- `C(k, k) = 1` — solo hay una forma de elegir k cosas de un conjunto de k elementos (el conjunto completo).

### Implementación (bottom-up con tabla)

```java
long binomial_coefficient(int n, int m) {
    long[][] bc = new long[MAXN + 1][MAXN + 1];

    for (int i = 0; i <= n; i++) bc[i][0] = 1;   // caso base: C(i,0)=1
    for (int j = 0; j <= n; j++) bc[j][j] = 1;   // caso base: C(j,j)=1

    for (int i = 1; i <= n; i++) {
        for (int j = 1; j < i; j++) {
            bc[i][j] = bc[i - 1][j - 1] + bc[i - 1][j];   // recurrencia de Pascal
        }
    }
    return bc[n][m];
}
```

Complejidad `O(n²)`, sin riesgo de overflow intermedio, y sin recursión repetida.

---

## Idea final

Los dos ejemplos siguen el mismo patrón de diseño de DP:
1. Encontrar la **recurrencia correcta** (a menudo la parte más difícil).
2. Identificar los **casos base**.
3. Implementarla **bottom-up** llenando una tabla (1D para Fibonacci, 2D para binomiales), en vez de recursar ingenuamente.

Este es el mismo patrón que ya viste en la simulación de Edit Distance (`simulador_edit_distance_dp.html`): primero la versión recursiva pura, luego la tabla `D[i][j]` llenada de abajo hacia arriba.
