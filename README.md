# CLASE 4
## Diseño de Sistemas de Transmisión para Control de Movimiento  

---

## Propósito General de los sistemas de transmisión 

Diseñar una transmisión adecuada para garantizar que un sistema cumpla con los requisitos de movimiento deseado, equilibrando torque, velocidad e inercia, tanto si se parte de una carga conocida como si se cuenta previamente con un motor o transmisión.

---

## Etapas del Proceso de Diseño  

| Fase | Descripción |
|------|-------------|
| 1 | Especificar los requerimientos de la carga (masa, velocidad, torque). |
| 2 | Determinar la relación de transmisión necesaria y calcular la inercia y torque reflejados. |

---

## Casos de Diseño  

1. **Diseño completo:** Se conoce el movimiento requerido de la carga. Es necesario seleccionar el motor y diseñar la transmisión.  
2. **Sistema existente:** Se tiene un motor y transmisión, y se desea conocer el comportamiento de la carga.  
3. **Motor fijo, carga deseada:** Se tiene un motor definido y una meta de movimiento para la carga. Se diseña la transmisión en función de esto.  
4. **Carga definida, transmisión fija:** Se elige un motor que se ajuste al movimiento deseado, usando una transmisión ya establecida.

---

## Inercia y Torque Reflejado

- La inercia determina la resistencia de un sistema a cambios en su velocidad angular:  
  $∑T=J·α$

- Se aplica tanto en rotación como en traslación.  
- La relación de transmisión afecta directamente cómo se refleja la inercia desde la carga hacia el motor.

---

## Transmisiones Mecánicas

### Engranajes


- Relación de velocidades angulares:  
  $ω_m/ω_l=r_l/r_m$

- Relación de transmisión (también en función del número de dientes):  
  $N_{GB}=n_l/n_m=r_l/r_m=ω_m/ω_l=T_l/T_m$

- Potencia:  
  $P=T_m·ω_m=T_l·ω_l$

#### Reflejo de Inercia y Torque

- Inercia reflejada:  
  $J_{ref}=J_{load}/N_{GB}^2$

- Torque reflejado:  
  $T_m=T_l/N_{GB}$

#### Consideraciones de Eficiencia

- Eficiencia del sistema:  
  $η=P_{salida}/P_{entrada}$

- Inercia reflejada considerando pérdidas:  
  $J_{ref}=J_{load}/(η·N_{GB}^2)$

- Torque reflejado con eficiencia:  
  $T_m=T_l/(η·N_{GB})$

---

### Cálculo de Inercia Total en el Motor

$J_{total}=J_m+J_{eje}+J_{ref}$

Donde:
- $J_m$: Inercia del rotor del motor  
- $J_{eje}$: Inercia del acoplamiento y componentes en el eje  
- $J_{ref}$: Inercia reflejada de la carga a través de la transmisión  

---

### Simulaciones

Simulink  

![Figura de prueba](IMAGES/simulink.png)

Simscape Multibody

![Figura de prueba](IMAGES/multibody.png)

---
### Ejemplo 

El Sistema en la figura usa un engranaje PN023 de Apex Dynamics. Este tiene 5:1 de relación, 0,15 Kg − cm2 reflejado a la entrada y 97% de eficiencia. El motor es un Quantum QB02301 NEMA tamaño 23 de Allied Motion Technologies. Este tiene 1,5x10−5 Kg − m2 de inercia en el rotor. Si la inercia de la carga es 10x10−4 Kg − m2. Encuentre la relación de inercia.

**Datos:**
- $N_{GB}=5$ 
- $η=0.97$  
- $J_m=1.5×10^{-5}\ kg·m^2$
- $J_{load}=10×10^{-4}\ kg·m^2$
- $J_{GB→M}=0.15×10^{-4}$

**Cálculos:**  

$J_{ref}=10×10^{-4}/(0.97·5^2)=4.124×10^{-5}$` 
$J_R=(4.124×10^{-5}+0.15×10^{-4})/(1.5×10^{-5})=3.75$

---

## Interpretación de la Relación de Inercia

La relación de inercia compara la carga que debe mover el motor respecto a su propia inercia:


$J_R=(J_{eje}+J_{ref})/J_m$

| Relación de inercia | Valor típico | Aplicación | Consideraciones |
|---------------------|--------------|------------|------------------|
| Baja (1–2)          | Rápido y preciso | Ideal para ciclos de parada y arranque frecuentes | Puede implicar sobredimensionamiento del motor |
| Alta (>10)          | Movimiento lento, sin precisión | Baja eficiencia o sobrecarga del motor | Riesgo de bajo rendimiento dinámico |

**Recomendación:** Mantener la relación de inercia entre 2 y 5 para un balance adecuado.

---

## Polea y Correa

Mecanismo rotacional que mantiene sentido de giro entre poleas.

### Relación de Transmisión:

$N_{BP}=ω_{ip}/ω_{lp}=r_{lp}/r_{ip}$

### Inercia Reflejada:

$J_{ref}=J_{IP}+(W_{belt}/(g·η))·r_{ip}^2+(1/(η·N_{BP}^2))·(J_{LP}+J_{load}+J_{C2})$


- La correa no tiene transmisión, su inercia se calcula como:  
$J=m·r^2=(W_{belt}/(g·η))·r_{ip}^2$

### Torque reflejado:

$T_{motor}=T_{carga}/(η·N_{BP})$

---

## Ejercicios  

## Ejercicios adicionales
### 1.
Un motor está acoplado a un engranaje con relación 6:1, eficiencia de 98%, y una inercia del engranaje de 0.12 kg·cm² reflejada a la entrada. El rotor tiene 3×10⁻⁵ kg·m² de inercia y la carga presenta una inercia de 1.2×10⁻³ kg·m².
Determina la relación de inercia $J_R$.

**Datos:**
- $N_{\text{GB}} = 6$
- $\eta = 0.98$
- $J_{\text{GB} \rightarrow M} = 0.12 \times 10^{-4} \ \text{kg·m}^2$
- $J_m = 3 \times 10^{-5}$
- $J_{\text{load}} = 1.2 \times 10^{-3}$

**1. Inercia reflejada:**

$$
J_{\text{load} \rightarrow M} = \frac{1.2 \times 10^{-3}}{0.98 \cdot 6^2}
= \frac{1.2 \times 10^{-3}}{35.28}
= 3.4 \times 10^{-5}
$$

**2. Relación de inercia:**

$$
J_R = \frac{0.12 \times 10^{-4} + 3.4 \times 10^{-5}}{3 \times 10^{-5}}
= \frac{4.6 \times 10^{-5}}{3 \times 10^{-5}}
= 1.53
$$

### 2.  

En un sistema, se usa un engranaje con relación 10:1, eficiencia del 96%, e inercia reflejada al motor de 0.18 kg·cm². El motor tiene una inercia de 2.5×10⁻⁵ kg·m² y la carga tiene 8×10⁻⁴ kg·m² de inercia.
Halla la inercia reflejada y la relación de inercia $J_R$.

**Datos:**
- $N_{\text{GB}} = 10$
- $\eta = 0.96$
- $J_{\text{GB} \rightarrow M} = 0.18 \times 10^{-4} \ \text{kg·m}^2$
- $J_m = 2.5 \times 10^{-5}$
- $J_{\text{load}} = 8 \times 10^{-4}$

**1. Inercia reflejada:**

$$
J_{\text{load} \rightarrow M} = \frac{8 \times 10^{-4}}{0.96 \cdot 10^2}
= \frac{8 \times 10^{-4}}{96}
= 8.33 \times 10^{-6}
$$

**2. Relación de inercia:**

$$
J_R = \frac{0.18 \times 10^{-4} + 8.33 \times 10^{-6}}{2.5 \times 10^{-5}}
= \frac{2.633 \times 10^{-5}}{2.5 \times 10^{-5}}
= 1.05
$$
---

## Conclusiones

- El análisis de inercia y torque es clave para un diseño exitoso.
- La relación de transmisión permite adaptar el sistema para responder a distintas cargas.
- La eficiencia debe tenerse en cuenta, ya que afecta el rendimiento real.
- Herramientas como Simulink y Simscape permiten validar estos diseños antes de implementarlos físicamente.
