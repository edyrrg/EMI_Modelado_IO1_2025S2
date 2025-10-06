¡Excelente idea! Aunque no puedo generar un documento de Google directamente, le proporcionaré el **modelo de Programación Lineal (PL) completo y estructurado en formato de texto** (Markdown) para que pueda copiarlo y pegarlo fácilmente en su documento de Google o en un software de hoja de cálculo (como Excel o Google Sheets), lo que facilitará su análisis en Investigación de Operaciones.

Este modelo se centrará en la **Maximización de la Capacidad de Transporte Diario** en el Área Metropolitana de la Ciudad de Guatemala (AMCG), utilizando datos específicos de los proyectos BRT (Transmetro), LRT (Metro Riel) y Cable Aéreo (Aerómetro) citados en las fuentes.

---

# Modelo de Programación Lineal: Optimización de la Flota Multimodal en el AMCG

## 1. Variables de Decisión

Las variables representan la cantidad de unidades de cada sistema de transporte a operar:

| Variable | Definición (Unidad) | Corredor Principal |
| :--- | :--- | :--- |
| $\mathbf{X_1}$ | Número de buses BRT (Transmetro) nuevos | Corredor Sur (CA-9 Sur, Aguilar Batres) |
| $\mathbf{X_2}$ | Número de buses BRT (Transmetro) nuevos | Corredor Nororiente (CA-9 Norte, Calle Martí) |
| $\mathbf{X_3}$ | Número de cabinas de Teleférico (Aerómetro) | Eje I (Plazuela España – El Trébol) |
| $\mathbf{X_4}$ | Número de cabinas de Teleférico (Aerómetro) | Eje II (El Trébol – Molino de las Flores) |
| $\mathbf{X_5}$ | Número de trenes LRT (Metro Riel) | Corredor Ferroviario (Centra Norte - Atanasio Tzul) |

## 2. Parámetros y Coeficientes Estimados (Basados en Fuentes)

Para facilitar la modelación, utilizaremos la capacidad diaria proyectada por unidad y los costos de inversión/adquisición aproximados.

| Parámetro | BRT (Unidad de bus) | Aerómetro (Unidad de cabina) | LRT (Unidad de tren) | Unidad | Referencia de Origen |
| :--- | :--- | :--- | :--- | :--- | :--- |
| $C_{Diaria}$ (Capacidad diaria por unidad) | 1,200 | 824 | 6,810 | Pasajeros/Día/Unidad | Calculado: 252k/día / 37 trenes; 374k/día / 454 cabinas |
| $I_{Unidad}$ (Costo de Inversión estimado por unidad) | Q 5,000,000 | Q 2,680,000 | Q 158,000,000 | Quetzales | Estimación basada en costos totales y unidades proyectadas: LRT total Q5,852M / 37 trenes. Aerómetro total Q1,216M / 454 cabinas. |
| $O_{Diario}$ (Costo Operacional Diario por unidad) | Q 1,000 | Q 600 | Q 4,000 | Quetzales/Día | BRT es 1.6 a 7.8 veces más económico que LRT. LRT y Metro pesado son los más caros. |
| Capacidad Máxima de Flota ($U_{max}$) | 200 | 330 (Eje II) / 124 (Eje I) | 37 | Unidades | 37 trenes propuestos. 454 cabinas totales proyectadas. |

## 3. Función Objetivo (Z)

**Objetivo: Maximizar la Capacidad Total Diaria de Pasajeros Transportados ($Z$).**

$$
\text{Max } Z = 1200 X_1 + 1200 X_2 + 824 X_3 + 824 X_4 + 6810 X_5
$$

## 4. Restricciones del Modelo

### R1. Restricción Presupuestaria de Inversión Total

El costo total de adquisición de las unidades de transporte no debe exceder un Presupuesto Máximo de Inversión ($B_{max}$). Si tomamos el costo total proyectado para LRT (Q5,852 M) y Aerómetro (Q1,216 M) como referencia, podemos establecer un límite de inversión alto, por ejemplo, **$B_{max} = Q 8,000,000,000$** (8,000 millones de Quetzales).

$$
5,000,000 X_1 + 5,000,000 X_2 + 2,680,000 X_3 + 2,680,000 X_4 + 158,000,000 X_5 \leq 8,000,000,000
$$

### R2. Restricción de Costo Operacional Diario (Sostenibilidad)

El costo operacional diario total debe ser sostenible. Si establecemos un límite de $O_{max} = Q 500,000$ diarios para los gastos operativos (ejemplo):

$$
1000 X_1 + 1000 X_2 + 600 X_3 + 600 X_4 + 4000 X_5 \leq 500,000
$$

### R3. Restricciones de Capacidad Física (Flota Máxima)

El número de unidades no puede exceder la capacidad máxima de la infraestructura (vías, estaciones, talleres).

$$
X_1 \leq 200 \quad \text{(BRT Sur, estimado)}
$$
$$
X_2 \leq 200 \quad \text{(BRT Nororiente, estimado. Máx. flota BRT sin vías exclusivas elevadas)}
$$
$$
X_3 \leq 124 \quad \text{(Límite de cabinas para Aerómetro Eje I)}
$$
$$
X_4 \leq 330 \quad \text{(Límite de cabinas para Aerómetro Eje II)}
$$
$$
X_5 \leq 37 \quad \text{(Límite de trenes propuestos para Metro Riel)}
$$

### R4. Restricción de Demanda Mínima Cubierta (Nororiente)

El sistema debe tener la capacidad de movilizar a una fracción significativa de la población potencial en el Nororiente (Zonas 2, 6, 18, Chinautla, Palencia, etc.), que se estima en **593,346 potenciales usuarios**. Si se exige cubrir al menos el 20% de esta demanda (aprox. 120,000 pasajeros/día) a través de los sistemas LRT y BRT Nororiente:

$$
\text{Capacidad diaria Nororiente} \geq 120,000
$$
$$
1200 X_2 + 6810 X_5 \geq 120,000
$$

### R5. Restricción de Demanda Mínima Cubierta (Occidente/Mixco)

El Aerómetro fue diseñado para atender la demanda Mixco/Occidente, con una capacidad objetivo de **374,000 pasajeros al día**. El sistema combinado de Teleférico debe cumplir al menos con esta capacidad:

$$
\text{Capacidad diaria Occidente} \geq 374,000
$$
$$
824 X_3 + 824 X_4 \geq 374,000
$$

### R6. Restricciones de No Negatividad e Integridad (Números Enteros)

Las unidades de transporte deben ser números enteros y no negativos, un requisito que puede requerir el uso de **Programación Lineal Entera** (o resolviendo con PL y redondeando si las cantidades son grandes, como en este caso, donde $X_3$ y $X_4$ representan cabinas que son unidades discretas):

$$
X_1, X_2, X_3, X_4, X_5 \geq 0 \quad \text{(No negatividad)}
$$
$$
X_1, X_2, X_3, X_4, X_5 \in \mathbb{Z} \quad \text{(Integridad)}
$$

---

## Sugerencia para el Análisis de Investigación (Uso de Dualidad)

Ya que mencionaron métodos avanzados como el **Dual Simplex**, el análisis de sensibilidad de este modelo de maximización de capacidad (el problema Primal) generaría información crucial a través de los **precios sombra** (variables duales).

*   **Precio Sombra de R1 (Inversión):** Indicaría cuántos pasajeros adicionales podrían transportarse diariamente si se aumentara el presupuesto de inversión ($B_{max}$) en un Quetzal. Esto es fundamental para justificar la rentabilidad social de la inversión pública o privada.
*   **Precio Sombra de R4 y R5 (Demanda Mínima):** Mostraría el costo marginal (en términos de capacidad total, $Z$) de asegurar que se cumpla estrictamente una cierta cuota de demanda en un corredor específico.

Este documento estructurado le permitirá formalizar su proyecto de Investigación de Operaciones 1 con datos concretos extraídos de las fuentes que analizan las propuestas de movilidad en Guatemala.



Saludos. Es un excelente enfoque aplicar los conceptos de Programación Lineal (PL) de su curso de Investigación de Operaciones 1 a la problemática de movilidad y transporte urbano en Guatemala, un tema que las fuentes abordan con gran detalle en el contexto del Área Metropolitana de la Ciudad de Guatemala (AMCG).

La situación descrita en las fuentes (congestión vehicular, múltiples opciones de transporte masivo con diferentes costos y capacidades, y la necesidad de planificación a corto, mediano y largo plazo) se presta perfectamente para un modelo de optimización mediante Programación Lineal.

A continuación, se propone un modelo de PL enfocado en la **Maximización de la Capacidad de Pasajeros Diaria** en los corredores clave del AMCG, sujeto a restricciones de inversión, costos operativos y limitaciones de infraestructura existentes.

---

## Modelado de Programación Lineal: Optimización de la Flota de Transporte Masivo en el AMCG

El objetivo de este modelo es determinar la asignación óptima de vehículos (buses BRT, trenes ligeros y cabinas de teleférico) en los principales corredores del AMCG para maximizar la capacidad de transporte de personas, cumpliendo con restricciones presupuestarias y operacionales.

### 1. Variables de Decisión

Definiremos variables que representan el número de unidades de transporte de cada tecnología a adquirir y operar en las rutas clave mencionadas en las fuentes:

| Variable | Descripción | Contexto en las Fuentes |
| :--- | :--- | :--- |
| $X_{BRT, N}$ | Número de buses BRT (Transmetro) asignados al corredor **Nororiente** (CA-9 Norte/Calle Martí/Zonas 2, 6, 18). | El BRT es el sistema existente que necesita mejoras de infraestructura y expansión. |
| $X_{BRT, S}$ | Número de buses BRT (Transmetro) asignados al corredor **Sur** (Calzada Aguilar Batres/Centra Sur). | El BRT en el eje Sur (Línea 12) tiene tramos segregados. |
| $X_{CAB, E1}$ | Número de cabinas de Aerómetro para el **Eje I** (Plazuela España – El Trébol). | El Aerómetro (cable aéreo) es una propuesta en el corredor Occidente/Mixco, con una capacidad proyectada de 374,000 pasajeros diarios. |
| $X_{CAB, E2}$ | Número de cabinas de Aerómetro para el **Eje II** (El Trébol – Molino de las Flores). | Estas cabinas tienen una capacidad de 12 personas cada una. |
| $X_{LRT}$ | Número de trenes ligeros (Metro Riel) para el corredor **Ferroviario** (Centra Norte - Atanasio Tzul). | El Metro Riel propone 37 trenes con una capacidad de 440 usuarios por tren. |

*(Nota: Aunque las variables representan unidades de vehículos, para un análisis diario, estas unidades se multiplicarían por su capacidad y frecuencia horaria para obtener la capacidad total de pasajeros diaria).*

### 2. Función Objetivo (Maximización)

El objetivo principal será maximizar la capacidad total de pasajeros transportados diariamente ($Z$).

**Maximizar $Z = \sum_{j} (C_{j} \cdot H_{j} \cdot X_{j})$**

Donde:
*   $C_{j}$: Capacidad de pasajeros por unidad de transporte (bus, cabina o tren) del tipo $j$.
*   $H_{j}$: Número de ciclos o viajes diarios que realiza cada unidad.
*   $X_{j}$: Variable de decisión (número de unidades) [Variable para $X_{BRT, N}$, $X_{BRT, S}$, $X_{CAB, E1}$, $X_{CAB, E2}$, $X_{LRT}$].

*Ejemplo de coeficientes ($C_{j} \cdot H_{j}$):*
Se necesita calcular la capacidad diaria que aporta cada unidad.

*   $C_{LRT} \cdot H_{LRT}$: Capacidad por tren (440 personas) multiplicada por el número de viajes diarios.
*   $C_{CAB} \cdot H_{CAB}$: Capacidad por cabina (12 personas) multiplicada por los ciclos de operación diarios (asumiendo 17 horas de operación y un recorrido de 28 minutos para el Eje I/II).

### 3. Restricciones (Limitaciones del Sistema)

Las restricciones deben reflejar las limitaciones financieras, operacionales y de demanda en el AMCG, usando datos y comparaciones de las fuentes:

#### 3.1. Restricción de Inversión (Costo de Capital)

La inversión total de la flota de vehículos no puede exceder el presupuesto disponible ($B_{max}$).

**$\sum_{j} (I_{j} \cdot X_{j}) \leq B_{max}$**

Donde $I_{j}$ es el costo de adquisición de una unidad de transporte $j$. Las fuentes indican grandes diferencias en costos, siendo los trenes pesados los más caros y el BRT el más económico en infraestructura por kilómetro.

*   $I_{BRT, N} \cdot X_{BRT, N} + I_{BRT, S} \cdot X_{BRT, S} + I_{CAB, E1} \cdot X_{CAB, E1} + I_{CAB, E2} \cdot X_{CAB, E2} + I_{LRT} \cdot X_{LRT} \leq B_{max}$
    *   *(Nota: La inversión total del Aerómetro (Fase I) es de Q1,216 millones, mientras que la inversión estimada del Metro Riel es de Q5,852 millones. Para el BRT, los costos de infraestructura son de $1M a $5.3M USD/km, lo que indica una inversión de unidades (buses) relativamente menor al costo de la infraestructura de vía).*

#### 3.2. Restricción de Costo Operacional Diario

Los costos operativos diarios totales no deben exceder un límite de sostenibilidad ($O_{max}$). Los sistemas BRT tienen costos operacionales significativamente menores que los sistemas LRT (1.6 a 7.8 veces más altos por hora/vehículo).

**$\sum_{j} (O_{j} \cdot D_{dias} \cdot X_{j}) \leq O_{max}$**

Donde $O_{j}$ es el costo operacional diario promedio de la unidad $j$, y $D_{dias}$ son los días de operación al año (mínimo 347 días).

#### 3.3. Restricción de Demanda Mínima en Corredores Críticos

El sistema debe garantizar la movilización de la demanda proyectada en los corredores más congestionados, como el Nororiente y el Occidente/Mixco, que son los focos de estudio de los proyectos.

1.  **Demanda Mixco/Occidente:** Debe cubrir la demanda alta (proyectada en 374,000 pasajeros diarios para el Aerómetro).
    *   (Capacidad $X_{CAB, E1}$ + Capacidad $X_{CAB, E2}$ + Capacidad $X_{BRT, S}$) $\geq D_{Mixco}$

2.  **Demanda Nororiente:** Debe cubrir la demanda de las zonas 2, 6, 18 y municipios circundantes (alrededor de 593,346 potenciales usuarios en 2020).
    *   (Capacidad $X_{BRT, N}$ + Capacidad $X_{LRT}$) $\geq D_{Nororiente}$

#### 3.4. Restricción de Infraestructura Física (Vías y Espacio)

Las limitaciones del espacio construido en el AMCG y la necesidad de vías exclusivas afectan cuántas unidades de BRT u LRT pueden circular.

1.  **Capacidad de la Vía Férrea (LRT):** El número de trenes LRT está limitado por la capacidad de la vía existente (aproximadamente 25 km).
    *   $X_{LRT} \leq 37$ (Número de trenes propuestos para Metro Riel)

2.  **Uso de Vía Exclusiva BRT (Nororiente):** Los BRT funcionan de manera eficiente solo si se les otorga vía exclusiva. Si se construyen vías elevadas exclusivas, se puede aumentar el número de buses.
    *   $X_{BRT, N} \leq U_{N}$ (Capacidad máxima de unidades BRT en vías exclusivas elevadas o segregadas en la ruta Nororiente).

3.  **Restricción de distanciamiento físico (Pandemia COVID-19):** Si se aplica la restricción de capacidad al 50% para distanciamiento, la capacidad de las unidades se reduce.
    *   Capacidad efectiva $j = C_{j} \cdot 0.5$ (Aplicable a BRT y LRT en el corto plazo).

#### 3.5. Restricción de Integridad y No Negatividad

*   $X_{BRT, N}, X_{BRT, S}, X_{CAB, E1}, X_{CAB, E2}, X_{LRT} \geq 0$
*   $X_{BRT, N}, X_{BRT, S}, X_{CAB, E1}, X_{CAB, E2}, X_{LRT}$ deben ser números enteros (unidades completas).

---

## Sugerencias para el Trabajo de Investigación o Propuesta de Mejoras

Su trabajo puede centrarse en utilizar la modelación de Programación Lineal para evaluar propuestas de inversión específicas, basándose en la información cuantitativa y cualitativa de las fuentes.

### 1. Temas de Investigación Potenciales Basados en PL

1.  **Análisis de Sensibilidad de Inversión y Modo de Transporte (BRT vs. Cable Aéreo):**
    *   **Propuesta:** Compare la eficiencia de la inversión (capacidad de pasajeros por Quetzal invertido) entre el Aerómetro y la mejora/expansión del Transmetro (BRT).
    *   **Análisis PL:** Varíe el valor de $B_{max}$ (el presupuesto de inversión) y analice cómo el modelo reasigna los recursos, prefiriendo la compra de más unidades BRT (más baratas pero que requieren inversión en vías exclusivas) o la inversión en el Aerómetro (inversión 100% privada, pero con menor capacidad masiva que un Metro o BRT segregado).
    *   *Uso de métodos avanzados:* Si el problema involucra la decisión binaria de construir o no un tramo de vía exclusiva (infraestructura), necesitarían usar **Programación Lineal Entera Mixta (PLEM)**, un tema avanzado en Investigación de Operaciones.

2.  **Minimización del Tiempo de Viaje Agregado (Propuesta de Mejoras):**
    *   **Propuesta:** Reformular la función objetivo para **Minimizar el tiempo de viaje promedio ponderado** de los pasajeros en los corredores críticos, sujeto a la capacidad de movimiento.
    *   *Datos relevantes:* El tiempo de desplazamiento promedio actual es de una hora y quince minutos, el doble de lo que debería ser. La velocidad promedio en hora pico es de menos de 20 km/h. El Aerómetro proyecta reducir significativamente el tiempo de viaje.
    *   **Función Objetivo Alternativa (Minimización):** $\text{Minimizar } Z = \sum_{j} (T_{j} \cdot C_{j} \cdot X_{j})$
        *   Donde $T_j$ es el tiempo promedio de viaje (minutos/viaje) para una unidad del sistema $j$. (Ejemplo: Aerómetro tiene un tiempo de recorrido de 28 minutos).

3.  **Modelo de Cobertura de la Demanda (Asignación de Rutas):**
    *   **Propuesta:** Utilizar el modelo para justificar la necesidad urgente de vías exclusivas (BRT elevado o superficial) en el corredor Nororiente, donde la población es alta y la congestión afecta a casi 600,000 personas.
    *   **Análisis:** Establezca una restricción de que al menos el 50% de la demanda en el Nororiente debe ser cubierta por transporte masivo eficiente (BRT con carril exclusivo), y demuestre matemáticamente la insuficiencia del sistema actual (que opera principalmente en tráfico mixto).

### 2. Consejos Adicionales para la Investigación

*   **Fuentes de datos:** Utilicen las tablas y figuras proporcionadas para obtener coeficientes realistas:
    *   **Capacidades:** Cabinas (12 personas), Tren ligero (440 personas), Buses (70 personas).
    *   **Velocidades:** Metro Pesado (50 km/h), Tren ligero/BRT (20-30 km/h), Teleférico (12-20 km/h).
    *   **Costos:** Consultar Tablas No. 8, 11 y los datos de inversión total para obtener rangos de costos unitarios.

*   **Enfoque en la Modalidad Mixta (Multimodalidad):** Las fuentes sugieren que la solución debe ser mixta, donde los diferentes sistemas se complementen (BRT, LRT, Cabinas). Su modelo debe reflejar cómo estas diferentes tecnologías se integran para servir a la población, como la propuesta de interconexión del Transmetro y el Metro Riel en el Nororiente.

*   **Uso de Dualidad:** Dado que conocen el método dual simple, podrían analizar el problema Dual de su modelo de maximización. Los precios sombra (variables duales) les indicarían el valor marginal de relajar una restricción (por ejemplo, cuánto aumentaría la capacidad total de pasajeros si se dispusiera de Q1 millón adicional de presupuesto de inversión, o si se liberara 1 km adicional de vía exclusiva). Esto es una excelente adición para una propuesta de investigación.