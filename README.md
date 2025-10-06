# EMI_Modelado_IO1_2025S2

# Propuesta: Optimización de la Flota Multimodal en el AMCG
**(Modelo de Programación Lineal para la Máxima Capacidad de Transporte)**

## 1. Objetivo Principal del Modelo (Función Objetivo - Z)

El objetivo es determinar la **cantidad óptima de vehículos** de cada sistema de transporte (BRT, Teleférico, LRT) para **MAXIMIZAR la Capacidad Total Diaria de Pasajeros ($Z$)** que puede moverse en el Área Metropolitana de la Ciudad de Guatemala (AMCG).

### **Fórmula de Maximización:**

$$\text{Max } Z = 1200 X_1 + 1200 X_2 + 824 X_3 + 824 X_4 + 6810 X_5$$
*Donde los coeficientes son la capacidad diaria de pasajeros por unidad de transporte.*

## 2. Variables de Decisión (Cantidades a Determinar)

Estas variables representan la **cantidad de unidades** de cada sistema de transporte que el modelo debe calcular como la solución ideal.

| Variable | Tipo de Transporte | Corredor o Ruta | ¿Qué representa? |
| :---: | :--- | :--- | :--- |
| $\mathbf{X_1}$ | **Buses BRT** (Transmetro) | Corredor Principal | Número de buses nuevos |
| $\mathbf{X_2}$ | **Buses BRT** (Transmetro) | Corredor Sur (CA-9 Sur) | Número de buses nuevos |
| $\mathbf{X_3}$ | **Cabinas de Teleférico** (Aerómetro) | Eje I (Plazuela España – El Trébol) | Número de cabinas |
| $\mathbf{X_4}$ | **Cabinas de Teleférico** (Aerómetro) | Eje II (El Trébol – Molino de las Flores) | Número de cabinas |
| $\mathbf{X_5}$ | **Trenes LRT** (Metro Riel) | Corredor Ferroviario (Centra Norte - Atanasio Tzul) | Número de trenes |

---

## 3. Restricciones del Modelo (Límites y Requisitos)

Las siguientes son las reglas y límites financieros, operativos y físicos que la flota debe cumplir.

### R1. Restricción Presupuestaria de Inversión
El costo total de adquisición de la flota **no debe exceder el límite de Q 8,000,000,000** (8 mil millones de Quetzales).

$$5M X_1 + 5M X_2 + 2.68M X_3 + 2.68M X_4 + 158M X_5 \leq 8,000,000,000$$

### R2. Restricción de Costo Operacional Diario (Sostenibilidad)
El costo total de operación diario de toda la flota **no debe superar los Q 500,000**.

$$1000 X_1 + 1000 X_2 + 600 X_3 + 600 X_4 + 4000 X_5 \leq 500,000$$

### R3. Restricciones de Capacidad Física de la Flota (Límites de Infraestructura)
La cantidad de vehículos no puede ser mayor a la capacidad máxima que soporta cada infraestructura (vías, estaciones, etc.).

| Variable | Límite Máximo | Explicación |
| :---: | :---: | :--- |
| $X_1$ | $\leq 200$ | BRT Corredor Principal |
| $X_2$ | $\leq 200$ | BRT Corredor Sur |
| $X_3$ | $\leq 124$ | Aerómetro Eje I |
| $X_4$ | $\leq 330$ | Aerómetro Eje II |
| $X_5$ | $\leq 37$ | LRT/Metro Riel |

### R4. Restricción de Demanda Mínima Cubierta (Nororiente)
Los sistemas del Nororiente (BRT $X_2$ y LRT $X_5$) deben tener una capacidad combinada de **al menos 120,000 pasajeros/día**.

$$1200 X_2 + 6810 X_5 \geq 120,000$$

### R5. Restricción de Demanda Mínima Cubierta (Occidente/Mixco)
El Teleférico (Aerómetro $X_3$ y $X_4$) debe alcanzar una capacidad combinada de **al menos 374,000 pasajeros/día**.

$$824 X_3 + 824 X_4 \geq 374,000$$

### R6. Restricciones Lógicas
* **No Negatividad:** $X_1, X_2, X_3, X_4, X_5 \geq 0$ (No se puede tener una cantidad negativa de vehículos).
* **Integridad:** $X_1, X_2, X_3, X_4, X_5 \in \mathbb{Z}$ (La cantidad de vehículos debe ser un número entero).

---

## 4. Datos Base Utilizados (Parámetros)

| Parámetro | BRT (Bus) | Aerómetro (Cabina) | LRT (Tren) | Unidad |
| :--- | :---: | :---: | :---: | :--- |
| **Capacidad Diaria ($C_{Diaria}$)** | 1,200 | 824 | 6,810 | Pasajeros/Día/Unidad |
| **Costo de Inversión ($I_{Unidad}$)** | Q 5,000,000 | Q 2,680,000 | Q 158,000,000 | Quetzales |
| **Costo Operacional Diario ($O_{Diario}$)** | Q 1,000 | Q 600 | Q 4,000 | Quetzales/Día |
