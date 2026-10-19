# Formulario Física II (FB401) – Parcial

Semanas 1 a 5: carga y campo eléctrico, Ley de Gauss, potencial, capacitancia y dieléctricos, corriente y circuitos. Constantes: k = 9×10⁹ N·m²/C² · ε₀ = 8,85×10⁻¹² C²/N·m² · k = 1/(4πε₀) · e = 1,6×10⁻¹⁹ C · mₑ = 9,1×10⁻³¹ kg · mₚ = 1,67×10⁻²⁷ kg · 1 eV = 1,6×10⁻¹⁹ J · nC = 10⁻⁹, µC = 10⁻⁶, mC = 10⁻³ C.

## 1. Carga y fuerza eléctrica

- La carga se conserva (no se crea ni se destruye). Carga por conducción (contacto) y por inducción (sin contacto, la carga neta sigue siendo cero).
- **Ley de Coulomb**: F₁₂ = (1/4πε₀)(q₁q₂/r₁₂²) û₁₂, con r₁₂ = r₂ − r₁ y û = r₁₂/|r₁₂|. Cargas iguales se repelen y opuestas se atraen. Los signos solo dan la dirección.
- **En un medio**: ε = κε₀ y la fuerza es κ veces menor que en el vacío. No confundir k (Coulomb) con κ (constante dieléctrica).
- **Superposición**: F = Σ Fᵢ = q/(4πε₀) · Σ (qᵢ/rᵢ²) ûᵢ (suma vectorial).
- **Energía potencial de un par**: U = k q₁q₂/r. Para un sistema, sumar cada par una sola vez.

## 2. Campo eléctrico

- Definición: E = F/q₀, o F = qE.
- **Carga puntual**: E = (1/4πε₀)(q/r²) r̂. Sale de la carga positiva y entra a la negativa.
- **Distribución discreta**: E = Σ k qᵢ/rᵢ² ûᵢ.
- **Distribución continua**: E = ∫ k dq/r² û, con dq = λ dl (lineal), σ dS (superficial) o ρ dV (volumétrica). Se descompone en componentes y se aprovecha la simetría.
- **Anillo** (radio a, carga Q) sobre su eje: E = (1/4πε₀) Q x/(x²+a²)^{3/2} î.
- **Lámina infinita** (σ): E = σ/(2ε₀). Dos placas paralelas con ±σ: E = σ/ε₀ entre ellas.
- **Varilla sobre su eje** (carga Q, longitud ℓ, distancia a al extremo): F = kqQ/\[a(a+ℓ)\]. Para a ≫ ℓ, F → kqQ/a² (carga puntual). Con densidad lineal λ(x) = λ₀(1 + cx), se integra dF = kq λ(x) dx/(a+ℓ−x)².
- **Líneas de campo**: E es tangente a ellas, nacen en + (o en ∞) y mueren en − (o en ∞), nunca se cruzan, su densidad es proporcional a E y el número de líneas es proporcional a la carga.

### Dipolo eléctrico

- Momento dipolar: p = q·d (C·m), de la carga − hacia la +.
- En E uniforme: fuerza neta = 0, torque τ = p × E, |τ| = pE senφ.
- Energía potencial: U = −p·E = −pE cosφ. Mínima en φ = 0 (equilibrio estable) y máxima en φ = π.

## 3. Ley de Gauss

- **Flujo**: Φ = ∫ E·dA = ∫ E cosθ dA. Unidad: N·m²/C. En superficie plana con E uniforme: Φ = EA cosθ.
- **Ley de Gauss**: Φ = ∮ E·dA = Q\_enc/ε₀. Es independiente de la forma y el tamaño de la superficie, y las cargas fuera no aportan flujo neto.
- **Superficie cerrada sin carga encerrada**: Φ = 0 (dipolo: Q = 0, Φ = 0).
- **Carga puntual en el centro de un cubo**: cada cara recibe Φ = q/(6ε₀).
- **Cómo aplicarla**: elegir una superficie donde E sea paralelo o perpendicular a dA y de módulo constante (esfera, cilindro, caja).

| Geometría | Resultado |
| --- | --- |
| Esfera conductora (carga q, radio R) | E = 0 si r < R; E = kq/r² si r ≥ R |
| Esfera maciza uniforme, r < a | E = kqr/a³ |
| Línea infinita (λ) | E = λ/(2πε₀ r) |
| Lámina infinita (σ) | E = σ/(2ε₀) |
| Cilindro infinito con ρ(r) = ρ₀r/R, r < R | E = ρ₀r²/(3ε₀R) |
| Mismo cilindro, r > R | E = ρ₀R²/(3ε₀ r) |

Para densidad no uniforme, calcular Q\_enc = ∫ ρ dV (en cilindro dV = 2πrL dr; en esfera dV = 4πr² dr).

### Conductores en equilibrio electrostático

- E = 0 en el interior y la carga libre está en la superficie.
- El conductor es una región equipotencial (E = −∇V = 0, entonces V = cte).
- E en la superficie es perpendicular a ella.
- **Cavidad con carga q** dentro de un conductor neutro: aparece −q en la cara interna y +q en la externa. Si el conductor ya tenía carga, la carga externa es (carga total) + q.

## 4. Potencial eléctrico

- Energía potencial: dU = −q₀E·ds y ΔU = −q₀ ∫ E·ds. Trabajo del campo: W = −ΔU = q(V\_A − V\_B).
- **Potencial**: V = U/q (1 V = 1 J/C). ΔV = V\_B − V\_A = −∫ₐᴮ E·ds. Depende solo de los puntos inicial y final (fuerza conservativa).
- **Campo en función del potencial**: E = −∇V = −(∂V/∂x î + ∂V/∂y ĵ + ∂V/∂z k̂). E apunta hacia donde V disminuye y es perpendicular a las equipotenciales.
- **Campo uniforme**: ΔV = −E·d y E = |ΔV|/d. Si ds ⊥ E, entonces ΔV = 0.
- **Carga puntual** (V(∞) = 0): V = kq/r. Superposición: V = Σ kqᵢ/rᵢ (escalar, se suma con signo).
- **Distribución continua**: dV = (1/4πε₀) dq/r.
- **Barra de longitud ℓ y carga Q, punto P a distancia a sobre el eje y**: V = k(Q/ℓ) ln\[(ℓ + √(ℓ²+a²))/a\].
- **Barra de longitud L sobre el eje x, punto a distancia x de su extremo**: V = (Q/4πε₀L) ln\[(x+L)/x\], y E = −dV/dx = Q/\[4πε₀ x(x+L)\].
- **Esfera conductora**: V = kq/R si r ≤ R; V = kq/r si r > R.
- **Conservación de energía**: K\_A + U\_A = K\_B + U\_B. Para una carga q liberada del reposo en un campo uniforme: ½mv² = qEd.
- **Electronvolt**: 1 eV = 1,6×10⁻¹⁹ J.
- **Carga negativa**: puede ir a mayor V y bajar su U (ΔU = qΔV con q < 0).
- **V vs ΔV**: V es de un punto respecto a una referencia; ΔV compara dos puntos.

## 5. Capacitancia y dieléctricos

- **Definición**: C = Q/V (1 F = 1 C/V). El capacitor tiene +Q y −Q.
- **Placas paralelas**: C = ε₀A/d. Con dieléctrico: C = κC₀ = κε₀A/d = εA/d.
- **Energía**: U = Q²/2C = ½CV² = ½QV.
- **Densidad de energía**: u = ½ε₀E² en el vacío y u = ½κε₀E² = ½εE² con dieléctrico.
- **Serie**: 1/C\_eq = 1/C₁ + 1/C₂ + …, misma carga Q, los V se suman, C\_eq menor que cada una.
- **Paralelo**: C\_eq = C₁ + C₂ + …, mismo V, las Q se suman, C\_eq mayor que cada una.
- **Dieléctrico en la mitad del área** (A/2 con κ y A/2 con aire): son dos capacitores en paralelo, C\_eq = ε₀A(κ+1)/2d.
- **Dieléctrico insertado una longitud x** (placas de lado L): C(x) = (ε₀L/d)\[L + (κ−1)x\]. Se trata como paralelo.
- **Ley de Gauss en dieléctricos**: ∮ κE·dA = Q\_libre/ε₀, con E = E₀/κ. Se usa solo la carga libre. Carga inducida: σᵢ = σ(1 − 1/κ).
- **Ruptura**: V\_max = E\_max·d y Q\_max = C·V\_max = κε₀A E\_max.
- **Polarización**: los dipolos (polares o inducidos) se alinean con E y aparecen cargas ligadas superficiales que debilitan el campo dentro.

### Al insertar un dieléctrico κ (pregunta frecuente)

| Magnitud | Capacitor aislado (Q constante) | Con batería (V constante) |
| --- | --- | --- |
| Carga | igual | Q → κQ (la batería aporta carga) |
| Voltaje | V → V/κ | igual |
| Capacitancia | C → κC | C → κC |
| Energía | U → U/κ (baja) | U → κU (sube) |
| Campo E | E → E/κ | igual (E = V/d) |

### Fuerza sobre el dieléctrico

- **Q constante** (aislado): F = −dU/dx, con U = Q²/2C(x). Resulta F = (Q²/2C²)·dC/dx > 0, que **absorbe** al dieléctrico. El trabajo del campo es W = −ΔU > 0 y U baja.
- **V constante** (batería): F = +½V² dC/dx. Con C(x) lineal, F = (ε₀b/2d)(κ−1)V².

## 6. Corriente y resistencia

- **Corriente**: I = dQ/dt (1 A = 1 C/s). Sentido convencional: el del flujo de carga positiva (de mayor a menor potencial).
- **Portadores**: I = n|q|v\_d A. Densidad de corriente: J = I/A = n|q|v\_d (A/m²). I = ∫ J·dA. n tiene unidades 1/m³.
- **Corriente de convección**: J = ρv y J\_s = σv. **Densidad superficial**: J\_s = I/ℓ.
- **Ecuación de continuidad**: ∮ J·dA = −dQ/dt y ∇·J + ∂ρ/∂t = 0. En corriente estacionaria, ∇·J = 0.
- **Ley de Ohm puntual**: J = σE o E = ρJ, con ρ = 1/σ (Ω·m).
- **Resistencia**: R = ρL/A = L/(σA) (ley de Pouillet). V = IR (Ley de Ohm macroscópica).
- **Temperatura (metales)**: ρ(T) = ρ₀\[1 + α(T − T₀)\] y R(T) = R₀\[1 + α(T − T₀)\].
- **Semiconductores**: ρ(T) = A e^{β/T} (la resistividad baja al subir T).
- **Resistores**: serie R\_eq = ΣRᵢ y paralelo 1/R\_eq = Σ1/Rᵢ.
- **Código de colores**: dos dígitos, un multiplicador ×10ⁿ y tolerancia (dorado ±5%, plateado ±10%, sin banda ±20%).

### Transformación delta ↔ estrella

- Delta → estrella: R₁ = R\_B R\_C/(R\_A+R\_B+R\_C), R₂ = R\_A R\_C/(R\_A+R\_B+R\_C), R₃ = R\_A R\_B/(R\_A+R\_B+R\_C).
- Estrella → delta: R\_A = (R₁R₂+R₂R₃+R₁R₃)/R₁, R\_B = (…)/R₂, R\_C = (…)/R₃. El numerador es siempre la misma suma de productos de a pares.

## 7. Fuerza electromotriz, energía y circuitos

- **Potencia y Joule**: P = VI = I²R = V²/R (W). Energía disipada: E = I²R·t = (V²/R)t (J).
- **fem ideal**: V\_ab = ε. Potencia que entrega la fuente: P = εI.
- **Fuente real** (resistencia interna r): V\_ab = ε − Ir y I = ε/(R\_L + r).
- **Máxima transferencia de potencia**: R\_L = r.
- **Línea de transmisión**: para la misma potencia P = IV, al subir V baja I y las pérdidas I²R son mucho menores.
- **Kirchhoff**: nodos, ΣI\_entran = ΣI\_salen. Mallas, Σε + ΣIR = 0 (suma algebraica en una malla cerrada).
- **Puente de Wheatstone** (balanceado, I\_G = 0): R\_x = (R₃/R₁)R₂.

### Circuito RC

|  | Carga (con fem ε) | Descarga |
| --- | --- | --- |
| Carga | Q(t) = Cε(1 − e^{−t/RC}) | Q(t) = Q₀ e^{−t/RC} |
| Corriente | I(t) = (ε/R) e^{−t/RC} | I(t) = −(Q₀/RC) e^{−t/RC} |
| Valores límite | Q\_f = Cε, I₀ = ε/R | I₀ = V\_C/R |

- Constante de tiempo: τ = RC. En t = τ la carga llega a 63% (carga) o cae a 37% (descarga).
- Con t = 0 el capacitor es un corto circuito, y con t → ∞ es un circuito abierto (V\_C = ε, I = 0).
- Despejar R: R = −t/\[C ln(1 − q/Q\_f)\]. Tiempo para llegar a una fracción f de Q\_f: t = −RC ln(1 − f).

## 8. Conceptual rápido (preguntas tipo P1)

- **Coulomb vs gravitación**: Coulomb atrae y repele, k es enorme, aplica a cargas pequeñas. Gravitación solo atrae, G es muy pequeña, aplica a cuerpos masivos.
- **Conductor equipotencial**: E = −∇V = 0, así V es constante.
- **E ⊥ superficie del conductor**: si hubiera componente tangencial, las cargas libres se moverían.
- **Zapatos conductores en quirófano**: evitan la acumulación de carga estática y las chispas cerca de oxígeno puro (acelera la combustión).
- **Líneas de campo**: son construcciones de Faraday, como un andamio que ayuda a visualizar el campo.
- **Potenciómetro**: resistencia variable de tres terminales para ajustar V o I (volumen, brillo, velocidad de motores).
