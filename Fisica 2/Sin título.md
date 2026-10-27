# Problemas resueltos – Física II (FB401)

Problemas parecidos a los de los parciales 2025-I, 2025-II y 2026-I, con datos nuevos y solución paso a paso. Úsalos primero sin mirar la solución. Constantes: k = 9×10⁹ N·m²/C², ε₀ = 8,85×10⁻¹² C²/N·m².

## 1. Capacitores y dieléctricos

### Problema 1.1 – Dieléctrico parcialmente insertado (capacitor aislado)

Un capacitor de placas cuadradas de lado L = 10 cm y separación d = 2 mm se carga a V₀ = 500 V y se desconecta de la batería. Luego se inserta un dieléctrico κ = 4 hasta la mitad (x = L/2). Calcula a) la capacitancia y el voltaje finales, b) las energías inicial y final, c) la fuerza sobre el dieléctrico, d) el trabajo del campo hasta que quede totalmente dentro.

**Solución a).** Capacitor inicial y carga (constante, porque está aislado):

$$
C_0=\frac{\varepsilon_0L^{2}}{d}=4{,}425\times10^{-11}\ \mathrm{F}\qquad Q=C_0V_0=2{,}21\times10^{-8}\ \mathrm{C}
$$

Con x = L/2 son dos capacitores en paralelo:

$$
C(x)=\frac{\varepsilon_0L}{d}\left[L+(\kappa-1)x\right]=4{,}425\times10^{-10}\,(0{,}1+3\cdot0{,}05)=1{,}106\times10^{-10}\ \mathrm{F}
$$

$$
V=\frac{Q}{C}=\frac{2{,}21\times10^{-8}}{1{,}106\times10^{-10}}=200\ \mathrm{V}
$$

**Solución b).**

$$
U_0=\tfrac12C_0V_0^{2}=5{,}53\times10^{-6}\ \mathrm{J}\qquad U=\frac{Q^{2}}{2C}=2{,}21\times10^{-6}\ \mathrm{J}
$$

La energía baja a 40% porque C sube ×2,5.

**Solución c).** Con Q constante, F = −dU/dx:

$$
\frac{dC}{dx}=\frac{\varepsilon_0L(\kappa-1)}{d}=1{,}3275\times10^{-9}\ \mathrm{F/m}\qquad F=\frac{Q^{2}}{2C^{2}}\frac{dC}{dx}=2{,}66\times10^{-5}\ \mathrm{N}
$$

La fuerza es positiva: el capacitor absorbe al dieléctrico.

**Solución d).** Con el dieléctrico completo, U = U₀/κ:

$$
W=U_0-\frac{U_0}{\kappa}=5{,}53\times10^{-6}\left(1-\tfrac14\right)=4{,}15\times10^{-6}\ \mathrm{J}>0\qquad W=-\Delta U
$$

### Problema 1.2 – Aislado vs. con batería

Un capacitor de C = 2 µF se carga a V = 100 V. Se inserta un dieléctrico κ = 3 que llena todo el espacio. Halla Q, V y U finales si el capacitor a) está aislado, b) sigue conectado a la batería.

**Solución.** Valores iniciales:

$$
Q_0=CV=200\ \mu\mathrm{C}\qquad U_0=\tfrac12CV^{2}=10\ \mathrm{mJ}
$$

Aislado (Q constante): V = V₀/κ, U = U₀/κ.

$$
Q=200\ \mu\mathrm{C}\qquad V=\frac{100}{3}=33{,}3\ \mathrm{V}\qquad U=\frac{10}{3}=3{,}33\ \mathrm{mJ}
$$

Conectado (V constante): Q = κQ₀, U = κU₀. La batería aporta 400 µC adicionales.

$$
Q=600\ \mu\mathrm{C}\qquad V=100\ \mathrm{V}\qquad U=30\ \mathrm{mJ}
$$

## 2. Ley de Gauss

### Problema 2.1 – Esfera no conductora y cascarón conductor

Una esfera no conductora de radio a = 2 cm tiene carga uniforme +3 µC. Un cascarón conductor concéntrico (b = 4 cm, c = 6 cm) tiene carga total +1 µC. En equilibrio, calcula E en r = 1 cm, 3 cm, 5 cm y 8 cm, las cargas en las superficies interna y externa del cascarón y V en r = c.

**Solución.** Dentro de la esfera, Q_enc = q r³/a³:

$$
E(1\ \mathrm{cm})=\frac{kqr}{a^{3}}=\frac{9\times10^{9}\cdot3\times10^{-6}\cdot0{,}01}{(0{,}02)^{3}}=3{,}38\times10^{7}\ \mathrm{N/C}
$$

Entre la esfera y el cascarón se encierra toda la carga de la esfera:

$$
E(3\ \mathrm{cm})=\frac{kq}{r^{2}}=\frac{9\times10^{9}\cdot3\times10^{-6}}{(0{,}03)^{2}}=3{,}0\times10^{7}\ \mathrm{N/C}
$$

En r = 5 cm estamos dentro del conductor: E = 0. Eso obliga a una carga inducida en la cara interna de −3 µC. La carga total del cascarón es +1 µC:

$$
q_{int}=-3\ \mu\mathrm{C}\qquad q_{ext}=+1-(-3)=+4\ \mu\mathrm{C}
$$

Fuera del cascarón se encierra 3 + 1 = 4 µC:

$$
E(8\ \mathrm{cm})=\frac{k(4\times10^{-6})}{(0{,}08)^{2}}=5{,}63\times10^{6}\ \mathrm{N/C}\qquad V(c)=\frac{k(4\times10^{-6})}{0{,}06}=6{,}0\times10^{5}\ \mathrm{V}
$$

### Problema 2.2 – Cilindro con densidad no uniforme

Un cilindro infinito de radio R tiene ρ(r) = ρ₀ (r/R)². Halla E(r) dentro y fuera y verifica la continuidad en r = R.

**Solución.** Por simetría E es radial y Φ = E(2πrL). Carga encerrada por dentro, con dV = 2πrL dr:

$$
Q_{enc}=\int_0^r\rho_0\frac{r'^{2}}{R^{2}}\,2\pi r'L\,dr'=\frac{\pi\rho_0L\,r^{4}}{2R^{2}}
$$

$$
E(2\pi rL)=\frac{Q_{enc}}{\varepsilon_0}\;\Rightarrow\;E_{r<R}=\frac{\rho_0\,r^{3}}{4\varepsilon_0R^{2}}
$$

Por fuera se encierra toda la carga, Q = πρ₀LR²/2:

$$
E_{r>R}=\frac{\rho_0R^{2}}{4\varepsilon_0\,r}
$$

Continuidad: en r = R ambas dan ρ₀R/(4ε₀). La dirección es radial hacia afuera si ρ₀ > 0.

### Problema 2.3 – Carga en el vértice de un cubo

Una carga q está en un vértice de un cubo de arista L. Halla el flujo total por las 6 caras y por cada cara.

**Solución.** Ocho cubos iguales alrededor del vértice encierran la carga completa, así que el cubo recibe 1/8 del flujo total:

$$
\Phi_{cubo}=\frac{q}{8\varepsilon_0}
$$

Las 3 caras que contienen el vértice tienen Φ = 0 (E es paralelo a ellas). Las 3 caras restantes se reparten el flujo por simetría:

$$
\Phi_{cara}=\frac{1}{3}\cdot\frac{q}{8\varepsilon_0}=\frac{q}{24\varepsilon_0}
$$

## 3. Fuerza de una varilla sobre una carga

### Problema 3.1 – Densidad uniforme y densidad lineal

Una varilla de longitud L = 0,20 m con carga Q = 4 µC está sobre el eje x. Una carga q = 2 nC se ubica sobre el eje a d = 0,10 m de su extremo derecho. a) Halla la fuerza si la densidad es uniforme. b) Halla la fuerza si λ(x) crece linealmente desde λ₀ en el extremo izquierdo hasta 4λ₀ en el derecho (el más cercano a q).

**Solución a).** Con dq = λ dx y r = L + d − x:

$$
F=kq\lambda\int_0^L\frac{dx}{(L+d-x)^{2}}=\frac{kqQ}{d\,(L+d)}=\frac{9\times10^{9}\cdot2\times10^{-9}\cdot4\times10^{-6}}{0{,}1\cdot0{,}3}=2{,}4\times10^{-3}\ \mathrm{N}
$$

**Solución b).** Condición de frontera λ(L) = 4λ₀ da λ(x) = λ₀(1 + 3x/L). Se halla λ₀ con la carga total:

$$
Q=\int_0^L\lambda_0\left(1+\frac{3x}{L}\right)dx=2{,}5\,\lambda_0L\;\Rightarrow\;\lambda_0=\frac{4\times10^{-6}}{2{,}5\cdot0{,}2}=8\times10^{-6}\ \mathrm{C/m}
$$

La integral de la fuerza (con u = L + d − x, y x = L + d − u):

$$
F=kq\lambda_0\int_0^L\frac{1+3x/L}{(L+d-x)^{2}}\,dx=kq\lambda_0\int_{d}^{L+d}\frac{5{,}5-15u}{u^{2}}\,du
$$

$$
\int_{d}^{L+d}\frac{5{,}5-15u}{u^{2}}\,du=5{,}5\left(\frac{1}{0{,}1}-\frac{1}{0{,}3}\right)-15\ln 3=36{,}67-16{,}48=20{,}19
$$

$$
F=9\times10^{9}\cdot2\times10^{-9}\cdot8\times10^{-6}\cdot20{,}19=2{,}9\times10^{-3}\ \mathrm{N}
$$

Es mayor que en a) porque la carga se concentra cerca de q.

## 4. Potencial y energía

### Problema 4.1 – Barra: potencial y campo en el eje

Una barra de longitud L = 0,5 m con Q = 10 nC está sobre el eje x. Halla V y E en un punto del eje a x = 0,25 m de su extremo cercano.

**Solución.**

$$
V=\frac{kQ}{L}\ln\!\left(\frac{x+L}{x}\right)=\frac{9\times10^{9}\cdot10^{-8}}{0{,}5}\ln 3=180\cdot1{,}0986=198\ \mathrm{V}
$$

$$
E=-\frac{dV}{dx}=\frac{kQ}{x\,(x+L)}=\frac{90}{0{,}25\cdot0{,}75}=480\ \mathrm{N/C}
$$

### Problema 4.2 – Energía potencial de un cuadrado de cargas

Cuatro cargas de magnitud q = 2 µC se ubican en los vértices de un cuadrado de lado a = 10 cm, con signos alternados (+ − + −). Halla la energía potencial del sistema.

**Solución.** Se suman los 6 pares una sola vez. Hay 4 lados (cargas opuestas, distancia a) y 2 diagonales (cargas iguales, distancia √2 a):

$$
U=\frac{kq^{2}}{a}\left(-4+\frac{2}{\sqrt2}\right)=\frac{kq^{2}}{a}\left(-4+\sqrt2\right)
$$

$$
\frac{kq^{2}}{a}=\frac{9\times10^{9}\cdot(2\times10^{-6})^{2}}{0{,}1}=0{,}36\ \mathrm{J}\;\Rightarrow\;U=0{,}36\,(-2{,}586)=-0{,}93\ \mathrm{J}
$$

El signo negativo indica un sistema ligado: se necesita trabajo externo para separarlo.

### Problema 4.3 – Oscilación de una carga entre dos cargas fijas

Dos cargas +q = 1 µC están fijas a d = 10 cm. Una carga −Q = −1 nC de masa m = 1 g se mueve sobre el bisector perpendicular, con x ≪ d. Halla el periodo y la rapidez al pasar por el punto medio si se suelta a a = 2 mm.

**Solución.** Para x ≪ d la fuerza restauradora es lineal y ω² = 16kqQ/(md³):

$$
\omega^{2}=\frac{16kqQ}{m\,d^{3}}=\frac{16\cdot9\times10^{9}\cdot10^{-6}\cdot10^{-9}}{10^{-3}\cdot10^{-3}}=144\;\Rightarrow\;\omega=12\ \mathrm{rad/s}
$$

$$
T=\frac{2\pi}{\omega}=0{,}524\ \mathrm{s}\qquad v_{max}=\omega a=12\cdot0{,}002=0{,}024\ \mathrm{m/s}
$$

## 5. Corriente y circuitos

### Problema 5.1 – Circuito RC

Un capacitor de C = 4,7 µF, inicialmente descargado, se conecta a una fem ε = 12 V a través de una resistencia R. Tras 1,5 ms la carga es 35 µC. Halla a) la carga final, b) R, c) el tiempo para llegar a 99% de la carga final, d) la corriente a los 1,5 ms.

**Solución a).**

$$
Q_f=C\varepsilon=4{,}7\times10^{-6}\cdot12=56{,}4\ \mu\mathrm{C}
$$

**Solución b).** De q = Q_f(1 − e^{−t/RC}):

$$
R=\frac{-t}{C\ln(1-q/Q_f)}=\frac{-1{,}5\times10^{-3}}{4{,}7\times10^{-6}\cdot\ln(0{,}3794)}=329\ \Omega\qquad \tau=RC=1{,}55\ \mathrm{ms}
$$

**Solución c).**

$$
t=-\tau\ln(0{,}01)=1{,}55\times10^{-3}\cdot4{,}605=7{,}1\ \mathrm{ms}
$$

**Solución d).**

$$
I=\frac{\varepsilon}{R}e^{-t/\tau}=\frac{12}{329}\,e^{-0{,}97}=36{,}5\ \mathrm{mA}\cdot0{,}379=13{,}8\ \mathrm{mA}
$$

Control de energía: la batería entrega Q_fε = 677 µJ; el capacitor guarda ½Cε² = 338 µJ y la otra mitad se disipa en R.

### Problema 5.2 – Resistencia equivalente de un puente

Entre a y b hay cinco resistores: a–x = 2 Ω, x–b = 4 Ω, a–y = 6 Ω, y–b = 3 Ω y x–y = 1 Ω. Halla R_eq entre a y b. ¿Qué valor de la resistencia y–b equilibraría el puente y cuánto sería entonces R_eq?

**Solución.** Se pone V_a = V y V_b = 0 y se aplica la regla de nodos en x e y:

$$
\text{nodo }x:\ \frac{V-V_x}{2}=\frac{V_x}{4}+\frac{V_x-V_y}{1}\;\Rightarrow\;2V=7V_x-4V_y
$$

$$
\text{nodo }y:\ \frac{V-V_y}{6}+\frac{V_x-V_y}{1}=\frac{V_y}{3}\;\Rightarrow\;V+6V_x=9V_y
$$

Resolviendo: V_x = 22V/39 y V_y = 19V/39. La corriente total sale por a:

$$
I=\frac{V-V_x}{2}+\frac{V-V_y}{6}=\frac{17}{78}V+\frac{10}{117}V=\frac{71}{234}V\;\Rightarrow\;R_{eq}=\frac{234}{71}=3{,}30\ \Omega
$$

Para equilibrar se exige R₁/R₃ = R₂/R₄, es decir, 2/6 = 4/R₄:

$$
R_4=\frac{R_2R_3}{R_1}=12\ \Omega\qquad R_{eq}=(2+4)\parallel(6+12)=\frac{6\cdot18}{24}=4{,}5\ \Omega
$$

En el puente equilibrado no circula corriente por la resistencia de 1 Ω y se puede ignorar.

### Problema 5.3 – Haz de electrones

Un haz de electrones tiene sección circular de radio 2,00 mm y corriente de 5,00 µA. Halla la densidad de corriente (uniforme) y el tiempo que tardan en emerger N_A = 6,022×10²³ electrones. Toma v ≈ c.

**Solución.**

$$
A=\pi r^{2}=\pi(2\times10^{-3})^{2}=1{,}257\times10^{-5}\ \mathrm{m^2}\qquad J=\frac{I}{A}=\frac{5\times10^{-6}}{1{,}257\times10^{-5}}=0{,}398\ \mathrm{A/m^2}
$$

Electrones por segundo: I/e. Entonces:

$$
\frac{I}{e}=\frac{5\times10^{-6}}{1{,}6\times10^{-19}}=3{,}13\times10^{13}\ \mathrm{s^{-1}}\qquad \Delta t=\frac{N_A}{I/e}=\frac{6{,}022\times10^{23}}{3{,}13\times10^{13}}=1{,}9\times10^{10}\ \mathrm{s}
$$

La rapidez c no se necesita para este tiempo; solo sirve para hallar n (n = I/(e v A)).
