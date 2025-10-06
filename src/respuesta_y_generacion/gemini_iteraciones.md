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


¡Absolutamente! El modelo de programación lineal es **sólido y está bien estructurado**. Para que tu propuesta sea aún más persuasiva y profesional, aquí tienes algunas sugerencias clave:

## Sugerencias para el Contenido y la Presentación de la Propuesta

---

### 1. **Contexto Ejecutivo y Relevancia (Al Inicio)** 📝

Añade una sección muy corta al principio (un párrafo) que responda a: **¿Por qué es importante este modelo?**

* **Título sugerido:** **Resumen Ejecutivo / Planteamiento del Problema**
* **Enfoque:** Enfatiza que la congestión vehicular es crítica y que este modelo es la herramienta científica para optimizar la **inversión limitada** y **maximizar el beneficio social** (pasajeros movilizados) de la flota de transporte multimodal en el AMCG. Muestra que tu enfoque es *estratégico*, no solo técnico.

---

### 2. **Justificación de Parámetros Clave** (Sección 4) 🔍

Los valores de capacidad y costos son cruciales. Tu propuesta será más creíble si explicas brevemente cómo se obtuvieron esos números, ya que esto da peso a las restricciones.

* **Añade una columna de "Fuente/Base del Cálculo"** a la tabla de Parámetros para mostrar de dónde vienen los datos ($C_{Diaria}$, $I_{Unidad}$, $O_{Diario}$). (Ya lo tienes en el original, asegúrate de mantenerlo claro en el documento final).
* **Justifica el presupuesto total ($B_{max}$):** Menciona por qué $Q 8,000,000,000$ es un límite realista o estratégico (p. ej., "El límite se estableció ligeramente por encima de los costos proyectados combinados para permitir flexibilidad en la adquisición").

---

### 3. **Claridad en las Restricciones de Demanda (R4 y R5)** 🎯

Las restricciones de demanda mínima son las que obligan al modelo a ser socialmente responsable. Hazlas más claras:

* **Usar Porcentajes:** En lugar de solo el número, recuerda mencionar el porcentaje que representa. Por ejemplo:
    * **R4 (Nororiente):** Exigir una capacidad de 120,000 pasajeros/día es equivalente a cubrir al menos el **20% de la demanda potencial** de esa área.
    * **R5 (Occidente):** La capacidad mínima es **374,000 pasajeros/día**, que es el **100% de la capacidad de diseño original** para el Aerómetro.

---

### 4. **Análisis de Impacto (Post-Modelo)** ✨

Si bien el modelo solo llega hasta las restricciones, la propuesta debe sugerir qué hacer con el resultado. Agrega una sección final que anticipe los beneficios:

* **Título Sugerido:** **Próximos Pasos y Beneficios Esperados**
* **Enfoque:** Explica que la solución del modelo proporcionará:
    1.  La **Combinación Óptima** de buses, cabinas y trenes.
    2.  La **Máxima Capacidad de Transporte** posible dentro de las limitaciones financieras.
    3.  Una **Hoja de Ruta de Inversión** que balancea la eficiencia ($X_5$ por alta capacidad) con la cobertura ($X_3, X_4$ por menor costo unitario).

---

### 5. **Formato en Google Docs (Consejos Rápidos)** 🖌️

Cuando lo pegues en el documento:

* **Fórmulas:** Si Google Docs no soporta la representación LaTeX (`$$`...) directamente, considera usar un generador de imágenes de ecuaciones en línea (como [Codecogs](https://editor.codecogs.com/)) y pega las fórmulas ($Z$ y Restricciones) como imágenes. Esto mantiene el aspecto profesional de la notación matemática.
* **Encabezados:** Usa consistentemente los estilos de encabezado (Título 1, Título 2, etc.) para que la tabla de contenidos se genere automáticamente.

Con estos ajustes, tu propuesta no solo será técnicamente precisa, sino también **estratégicamente impactante y fácil de digerir** para quienes toman las decisiones.