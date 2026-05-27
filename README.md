# ETSformer aplicado al Pronóstico de Consumo Eléctrico

> Proyecto final del Diplomado — **Grupo 7**
> Aplicación práctica del paper *ETSformer: Exponential Smoothing Transformers for Time-series Forecasting* (Woo et al., 2022) a datos reales de consumo eléctrico.

---

## Descripción

Este proyecto demuestra la aplicación de **ETSformer**, una arquitectura híbrida que combina el suavizado exponencial clásico con la arquitectura Transformer, al problema de **pronóstico de consumo eléctrico** sobre datos reales del dataset `LD2011_2014`.

El objetivo es mostrar cómo un modelo moderno de series temporales puede generar valor en un caso de uso concreto del sector energético: anticipar la demanda eléctrica con horas de antelación para optimizar la planificación de la red, evitar picos críticos y reducir costos operativos.

---

## Estructura del repositorio

```
Grupo7/
├── README.md
├── ETSFormer Consumo Eléctrico_2026.ipynb   # Notebook con el experimento completo
└── ETSformer_Aplicacion.pptx                # Presentación final del proyecto
└── LD2011_2014.txt -> descargar link: https://drive.google.com/file/d/1yKZZhPZBy57ij_sp8aF59HikPW8E9q-T/view?usp=sharing
```

---

## Dataset

**LD2011_2014** — UCI Machine Learning Repository

| Característica | Valor |
|---|---|
| Fuente | UCI Machine Learning Repository |
| Origen | Mediciones de consumo eléctrico, Portugal |
| Periodo | 2011 – 2014 (4 años) |
| Frecuencia | 1 medición cada 15 minutos |
| Registros totales | 140,256 filas × 370 clientes |
| Cliente seleccionado | MT_362 (mayor consumo total) |
| Ventana de estudio | desde 2012-01-01 (105,217 registros) |
| Tipo de problema | Forecasting univariado |

Link del dataset: [UCI – Electricity Load Diagrams](https://archive.ics.uci.edu/ml/datasets/ElectricityLoadDiagrams20112014)

---

## Metodología

El pipeline completo del experimento:

1. **Carga de datos** desde el archivo `LD2011_2014.txt` (formato CSV con separador `;` y decimal europeo).
2. **Procesamiento de fecha**: conversión a `datetime` y ordenamiento cronológico.
3. **Selección de un cliente** con mayor consumo total → `MT_362`.
4. **Recorte temporal** desde 2012 para evitar tramos iniciales con muchos ceros.
5. **Exportación** a formato compatible con el repositorio oficial de ETSformer.
6. **Entrenamiento** del modelo con parámetros optimizados para demostración.
7. **Inferencia y visualización** de predicción vs valor real.

## Cómo ejecutar el notebook

### Requisitos

- Python 3.10+
- Acceso a un entorno tipo **Databricks** o Jupyter con GPU/CPU
- Dependencias: `torch`, `einops`, `tqdm`, `scipy`, `scikit-learn`, `matplotlib`, `pandas`, `numpy`

### Pasos

1. Clonar el repositorio oficial de ETSformer:
   ```bash
   git clone https://github.com/salesforce/ETSformer.git
   ```
2. Descargar el dataset `LD2011_2014.txt` desde UCI y colocarlo en la ruta indicada en el notebook.
3. Abrir y ejecutar `ETSFormer Consumo Eléctrico_2026.ipynb` celda por celda.

---

## Marco teórico (resumen)

**ETSformer** propone reemplazar la `self-attention` tradicional del Transformer por dos mecanismos nuevos:

- **ESA (Exponential Smoothing Attention)** — Asigna pesos a las observaciones pasadas en función del rezago temporal, con decaimiento exponencial. Modela el componente de crecimiento.
- **FA (Frequency Attention)** — Usa la transformada rápida de Fourier (FFT) para detectar las K frecuencias dominantes de la serie. Modela la estacionalidad sin requerir features manuales.

Ambos mecanismos mantienen complejidad **O(L · log L)**, igual de eficientes que Informer o Autoformer.

El modelo genera un pronóstico interpretable como suma explícita de tres componentes:

> **Forecast = Nivel + Crecimiento + Estacionalidad**

---

## Integrantes — Grupo 7

| Nombre |
|---|
| Analy del Milagro Quesquen Carvallo |
| Edgar Delgado Ortega |
| Enrique Alberto Gortaire Arboleda |
| Rodrigo Antonio Morocho Diaz |


*Diplomado · Mayo de 2026*
