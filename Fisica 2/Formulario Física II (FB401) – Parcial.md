# Formulario Física II (FB401) – Parcial

Fórmulas de las semanas 1 a 5 en LaTeX, con las constantes al inicio.

**Constantes**

$$
k=\frac{1}{4\pi\varepsilon_0}=9\times10^{9}\ \mathrm{N\,m^2/C^2}\qquad \varepsilon_0=8{,}85\times10^{-12}\ \mathrm{C^2/(N\,m^2)}
$$
$$e=1{,}6\times10^{-19}\ \mathrm{C}\qquad m_e=9{,}1\times10^{-31}\ \mathrm{kg}\qquad m_p=1{,}67\times10^{-27}\ \mathrm{kg}\qquad 1\ \mathrm{eV}=1{,}6\times10^{-19}\ \mathrm{J}$$
## 1. Carga y fuerza eléctrica

La carga se conserva y se transfiere por conducción (contacto) o por inducción (sin contacto). Cargas iguales se repelen y opuestas se atraen; los signos solo dan la dirección.

**Ley de Coulomb**

$$\vec F_{12}=\frac{1}{4\pi\varepsilon_0}\,\frac{q_1q_2}{r_{12}^{2}}\,\hat u_{12}\qquad \hat u_{12}=\frac{\vec r_2-\vec r_1}{\left|\vec r_2-\vec r_1\right|}
$$

**En un medio** (κ es la constante dieléctrica; no confundir con k)

$$\varepsilon=\kappa\,\varepsilon_0$$
**Superposición**

$$
\vec F=\sum_i \vec F_{iP}=\frac{q}{4\pi\varepsilon_0}\sum_i \frac{q_i}{r_{iP}^{2}}\,\hat u_{iP}$$

**Energía potencial de un par de cargas**

$$U=\frac{k\,q_1q_2}{r}$$

## 2. Campo eléctrico

**Definición y carga puntual**

```
\vec E=\frac{\vec F}{q_0}\qquad \vec F=q\vec E\qquad \vec E=\frac{1}{4\pi\varepsilon_0}\frac{q}{r^{2}}\,\hat r
```

**Distribución discreta**

```latex
\vec E=\sum_i \frac{1}{4\pi\varepsilon_0}\frac{q_i}{r_i^{2}}\,\hat u_i
```

**Distribución continua**

```latex
\vec E=\int k\,\frac{dq}{r^{2}}\,\hat u_r\qquad dq=\lambda\,d\ell=\sigma\,dS=\rho\,dV
```

**Anillo (radio a, carga Q) sobre su eje**

```latex
E_x=\frac{1}{4\pi\varepsilon_0}\,\frac{Q\,x}{\left(x^{2}+a^{2}\right)^{3/2}}
```

**Lámina infinita y placas paralelas con ±σ**

```latex
E=\frac{\sigma}{2\varepsilon_0}\qquad E_{\text{entre placas}}=\frac{\sigma}{\varepsilon_0}
```

**Varilla (carga Q, longitud ℓ) y carga q a distancia a de su extremo**

```latex
F=\frac{kqQ}{a\,(a+\ell)}\;\xrightarrow{\,a\gg\ell\,}\;\frac{kqQ}{a^{2}}
```

**Varilla con densidad lineal variable** (λ₀ en el extremo lejano, c fijado por la condición de frontera)

```latex
dF=\frac{kq\,\lambda(x)\,dx}{(a+\ell-x)^{2}}\qquad \lambda(x)=\lambda_0\left(1+c\,x\right)
```

Líneas de campo: E es tangente a ellas; nacen en cargas positivas (o en el infinito) y mueren en las negativas; nunca se cruzan; su densidad es proporcional a E.

### Dipolo eléctrico

```latex
p=q\,d\qquad \vec\tau=\vec p\times\vec E\qquad \tau=pE\sin\phi
```

```latex
U=-\vec p\cdot\vec E=-pE\cos\phi
```

En un campo uniforme la fuerza neta es cero. U es mínima en φ = 0 (equilibrio estable) y máxima en φ = π.

## 3. Ley de Gauss

**Flujo eléctrico** (unidad: N·m²/C)

```latex
\Phi=\int \vec E\cdot d\vec A=\int E\cos\theta\,dA\qquad \Phi=EA\cos\theta\ \text{(plano, E uniforme)}
```

**Ley de Gauss**

```latex
\oint \vec E\cdot d\vec A=\frac{Q_{enc}}{\varepsilon_0}
```

Es independiente de la forma y del tamaño de la superficie; las cargas fuera no aportan flujo neto. Sin carga encerrada, Φ = 0 (también para un dipolo). Se elige una superficie donde E sea paralelo o perpendicular a dA y de módulo constante.

**Carga puntual en el centro de un cubo** (flujo por cada cara)

```latex
\Phi_{cara}=\frac{q}{6\varepsilon_0}
```

**Carga encerrada con densidad no uniforme**

```latex
Q_{enc}=\int\rho\,dV\qquad dV_{cil}=2\pi r L\,dr\qquad dV_{esf}=4\pi r^{2}\,dr
```

**Esfera conductora (carga q, radio R)**

```latex
E=\begin{cases}0 & r<R\\[2pt] k\dfrac{q}{r^{2}} & r\ge R\end{cases}
```

**Esfera maciza con carga uniforme (radio a), dentro**

```latex
E=\frac{k\,q\,r}{a^{3}}\qquad (r<a)
```

**Línea infinita**

```latex
E=\frac{\lambda}{2\pi\varepsilon_0\,r}
```

**Cilindro infinito con ρ(r) = ρ₀ r/R**

```latex
E=\begin{cases}\dfrac{\rho_0\,r^{2}}{3\varepsilon_0 R} & r<R\\[6pt] \dfrac{\rho_0\,R^{2}}{3\varepsilon_0\,r} & r>R\end{cases}
```

### Conductores en equilibrio electrostático

- E = 0 en el interior y la carga libre está en la superficie.
- Es una región equipotencial porque E = −∇V = 0 implica V constante.
- E en la superficie es perpendicular a ella (una componente tangencial movería las cargas libres).
- Cavidad con carga q dentro de un conductor neutro: aparece −q en la cara interna y +q en la externa. Si el conductor ya tenía carga, la carga externa es (carga total) + q.

## 4. Potencial eléctrico

**Energía potencial y trabajo del campo**

```latex
\Delta U=-q_0\int_A^B \vec E\cdot d\vec s\qquad W=-\Delta U=q\,(V_A-V_B)
```

**Potencial y diferencia de potencial** (1 V = 1 J/C)

```latex
V=\frac{U}{q}\qquad \Delta V=V_B-V_A=-\int_A^B \vec E\cdot d\vec s
```

**Campo a partir del potencial**

```latex
\vec E=-\nabla V=-\left(\frac{\partial V}{\partial x}\,\hat\imath+\frac{\partial V}{\partial y}\,\hat\jmath+\frac{\partial V}{\partial z}\,\hat k\right)
```

E apunta hacia donde V disminuye y es perpendicular a las equipotenciales.

**Campo uniforme** (si ds ⊥ E, entonces ΔV = 0)

```latex
\Delta V=-E\,d\qquad E=\frac{|\Delta V|}{d}
```

**Carga puntual** (V = 0 en el infinito) y superposición

```latex
V=\frac{kq}{r}\qquad V_P=\sum_i\frac{kq_i}{r_i}\qquad dV=\frac{1}{4\pi\varepsilon_0}\frac{dq}{r}
```

**Barra de longitud ℓ y carga Q; punto P a distancia a sobre el eje y**

```latex
V_P=k\,\frac{Q}{\ell}\,\ln\!\left(\frac{\ell+\sqrt{\ell^{2}+a^{2}}}{a}\right)
```

**Barra de longitud L sobre el eje x; punto a distancia x de su extremo**

```latex
V(x)=\frac{Q}{4\pi\varepsilon_0 L}\,\ln\!\left(\frac{x+L}{x}\right)\qquad E(x)=-\frac{dV}{dx}=\frac{Q}{4\pi\varepsilon_0\,x\,(x+L)}
```

**Esfera conductora**

```latex
V=\begin{cases}k\dfrac{q}{R} & r\le R\\[6pt] k\dfrac{q}{r} & r>R\end{cases}
```

**Conservación de la energía** (y partícula liberada del reposo en campo uniforme)

```latex
K_A+U_A=K_B+U_B\qquad \tfrac12 m v^{2}=qEd
```

Una carga negativa puede ir hacia mayor V y bajar su energía potencial, porque ΔU = qΔV con q < 0. V es de un punto respecto a una referencia; ΔV compara dos puntos.

## 5. Capacitancia y dieléctricos

**Capacitancia y placas paralelas**

```latex
C=\frac{Q}{V}\qquad C_0=\frac{\varepsilon_0A}{d}\qquad C=\kappa C_0=\frac{\kappa\varepsilon_0A}{d}=\frac{\varepsilon A}{d}
```

**Energía y densidad de energía**

```latex
U=\frac{Q^{2}}{2C}=\tfrac12CV^{2}=\tfrac12QV\qquad u=\tfrac12\varepsilon_0E^{2}\ \text{(vacío)}\qquad u=\tfrac12\kappa\varepsilon_0E^{2}=\tfrac12\varepsilon E^{2}\ \text{(dieléctrico)}
```

**Serie** (misma Q, los V se suman, C\_eq menor que cada una)

```latex
\frac{1}{C_{eq}}=\frac{1}{C_1}+\frac{1}{C_2}+\cdots
```

**Paralelo** (mismo V, las Q se suman, C\_eq mayor que cada una)

```latex
C_{eq}=C_1+C_2+\cdots
```

**Dieléctrico en la mitad del área** (dos capacitores en paralelo)

```latex
C_{eq}=\frac{\kappa\varepsilon_0A}{2d}+\frac{\varepsilon_0A}{2d}=\frac{\varepsilon_0A}{2d}\,(\kappa+1)
```

**Dieléctrico insertado una longitud x** (placas de lado L y ancho b = L)

```latex
C(x)=\frac{\varepsilon_0 L}{d}\left[L+(\kappa-1)\,x\right]
```

**Ley de Gauss en dieléctricos** (solo cuenta la carga libre) y carga inducida

```latex
\oint \kappa\vec E\cdot d\vec A=\frac{Q_{libre}}{\varepsilon_0}\qquad E=\frac{E_0}{\kappa}\qquad \sigma_i=\sigma\left(1-\frac{1}{\kappa}\right)
```

**Ruptura del dieléctrico**

```latex
V_{max}=E_{max}\,d\qquad Q_{max}=\kappa\,\varepsilon_0\,A\,E_{max}
```

**Al insertar un dieléctrico κ (pregunta frecuente)**

| Magnitud | Aislado (Q constante) | Con batería (V constante) |
| --- | --- | --- |
| Carga | igual | sube ×κ (la batería aporta carga) |
| Voltaje | baja ÷κ | igual |
| Capacitancia | sube ×κ | sube ×κ |
| Energía | baja ÷κ | sube ×κ |
| Campo E | baja ÷κ | igual (E = V/d) |

**Fuerza sobre el dieléctrico, con Q constante (absorbe al dieléctrico)**

```latex
F=-\frac{dU}{dx}=\frac{Q^{2}}{2C^{2}}\,\frac{dC}{dx}>0\qquad W=-\Delta U>0
```

**Fuerza sobre el dieléctrico, con V constante**

```latex
F=\tfrac12V^{2}\,\frac{dC}{dx}=\frac{\varepsilon_0 b}{2d}\,(\kappa-1)\,V^{2}
```

## 6. Corriente y resistencia

**Corriente y densidad de corriente** (n en 1/m³; sentido convencional: carga positiva)

```latex
I=\frac{dQ}{dt}\qquad I=n|q|\,v_d\,A\qquad J=\frac{I}{A}=n|q|\,v_d\qquad I=\int \vec J\cdot d\vec A
```

**Corriente de convección**

```latex
\vec J=\rho\,\vec v\qquad \vec J_s=\sigma\,\vec v\qquad J_s=\frac{I}{\ell}
```

**Ecuación de continuidad** (corriente estacionaria: ∇·J = 0)

```latex
\oint \vec J\cdot d\vec A=-\frac{dQ}{dt}\qquad \nabla\cdot\vec J+\frac{\partial\rho}{\partial t}=0
```

**Ley de Ohm puntual y macroscópica**

```latex
\vec J=\sigma\vec E\qquad \vec E=\rho\vec J\qquad \rho=\frac{1}{\sigma}\qquad V=IR
```

**Resistencia (ley de Pouillet)**

```latex
R=\frac{\rho L}{A}=\frac{L}{\sigma A}
```

**Variación con la temperatura** (metales y semiconductores)

```latex
\rho(T)=\rho_0\left[1+\alpha\,(T-T_0)\right]\qquad R(T)=R_0\left[1+\alpha\,(T-T_0)\right]\qquad \rho_{semic}(T)=A\,e^{\beta/T}
```

**Resistores en serie y en paralelo**

```latex
R_{eq}=\sum_i R_i\qquad \frac{1}{R_{eq}}=\sum_i\frac{1}{R_i}
```

**Delta → estrella**

```latex
R_1=\frac{R_BR_C}{R_A+R_B+R_C}\qquad R_2=\frac{R_AR_C}{R_A+R_B+R_C}\qquad R_3=\frac{R_AR_B}{R_A+R_B+R_C}
```

**Estrella → delta**

```latex
R_A=\frac{R_1R_2+R_2R_3+R_1R_3}{R_1}\qquad R_B=\frac{R_1R_2+R_2R_3+R_1R_3}{R_2}\qquad R_C=\frac{R_1R_2+R_2R_3+R_1R_3}{R_3}
```

Código de colores: dos dígitos, un multiplicador ×10ⁿ y la tolerancia (dorado ±5%, plateado ±10%, sin banda ±20%).

## 7. Fuerza electromotriz y circuitos

**Potencia y efecto Joule**

```latex
P=VI=I^{2}R=\frac{V^{2}}{R}\qquad E=I^{2}R\,t
```

**Fuente real** (resistencia interna r) y potencia de la fuente

```latex
V_{ab}=\varepsilon-Ir\qquad I=\frac{\varepsilon}{R_L+r}\qquad P_{fuente}=\varepsilon I
```

**Máxima transferencia de potencia**

```latex
R_L=r
```

**Reglas de Kirchhoff**

```latex
\sum I_{entran}=\sum I_{salen}\qquad \sum_{malla}\Delta V=0
```

**Puente de Wheatstone balanceado** (corriente nula en el galvanómetro)

```latex
R_x=\frac{R_3}{R_1}\,R_2
```

**Circuito RC: carga con fem ε**

```latex
Q(t)=C\varepsilon\left(1-e^{-t/RC}\right)\qquad I(t)=\frac{\varepsilon}{R}\,e^{-t/RC}\qquad Q_f=C\varepsilon\qquad I_0=\frac{\varepsilon}{R}
```

**Circuito RC: descarga**

```latex
Q(t)=Q_0\,e^{-t/RC}\qquad I(t)=-\frac{Q_0}{RC}\,e^{-t/RC}\qquad I_0=\frac{V_C}{R}
```

**Constante de tiempo, resistencia y tiempo para llegar a una fracción f de Q\_f**

```latex
\tau=RC\qquad R=\frac{-t}{C\ln\!\left(1-q/Q_f\right)}\qquad t=-RC\,\ln(1-f)
```

En t = τ la carga llega a 63% (carga) o cae a 37% (descarga). Con t = 0 el capacitor es un corto circuito; con t → ∞ es un circuito abierto (V\_C = ε, I = 0).

## 8. Conceptual rápido (preguntas tipo P1)

- **Coulomb vs gravitación**: Coulomb atrae y repele, k es enorme y aplica a cargas pequeñas. Gravitación solo atrae, G es muy pequeña y aplica a cuerpos masivos.
- **Conductor equipotencial**: E = −∇V = 0, así que V es constante.
- **Zapatos conductores en quirófano**: evitan la acumulación de carga estática y chispas cerca de oxígeno puro, que acelera la combustión.
- **Líneas de campo**: son construcciones de Faraday, como un andamio que ayuda a visualizar el campo.
- **Línea de transmisión**: con la misma potencia P = IV, al subir V baja I y las pérdidas I²R son mucho menores.
- **Potenciómetro**: resistencia variable de tres terminales para ajustar V o I (volumen, brillo, velocidad de motores).
