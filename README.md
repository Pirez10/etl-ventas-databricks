# 📊 ETL de Ventas con PySpark en Databricks

## 🚀 Descripción

Este proyecto implementa un pipeline ETL utilizando PySpark en Databricks para procesar datos de ventas, enriquecerlos con información de productos y generar métricas agregadas listas para análisis.

El flujo sigue una arquitectura tipo **Medallion (Bronze → Silver → Gold)**, comúnmente utilizada en entornos de Data Engineering modernos.

---

## 🧱 Arquitectura del Proyecto

```
Bronze (datos crudos)
    ↓
Silver (datos limpios y transformados)
    ↓
Gold (métricas listas para negocio)
```

---

## ⚙️ Tecnologías utilizadas

* PySpark
* Databricks
* Delta Lake
* SQL

---

## 📂 Estructura del Proyecto

```
mi-proyecto/
│
├── notebooks/
│   ├── 01_extract
│   ├── 02_transform
│   ├── 03_load
│
├── src/
│   ├── transformations
│   ├── utils
│
├── data/
│   ├── raw/
│   ├── processed/
```

---

## 🔄 Pipeline ETL

### 🥉 1. Extract

* Generación / ingesta de datos de ventas y productos
* Almacenamiento en tablas Delta en la capa `bronze`

Tablas generadas:

* `bronze.ventas_raw`
* `bronze.productos`

---

### 🥈 2. Transform

* Limpieza de datos (filtrado de nulos y valores inválidos)
* Join con tabla de productos
* Generación de métricas:

  * Ventas totales por día
  * Clientes únicos
  * Promedio móvil de 7 días
  * Comparación con día anterior (window functions)

Salida:

* `silver.resumen_diario`

---

### 🥇 3. Load

* Validaciones de calidad de datos
* Escritura en formato Delta
* Generación de tabla final optimizada para análisis

Salida final:

* `gold.ventas_diarias`

---

## 📈 Ejemplo de métricas generadas

| fecha      | ventas_totales | clientes_unicos | ventas_7d | ventas_prev_dia |
| ---------- | -------------- | --------------- | --------- | --------------- |
| 2024-01-01 | 300            | 2               | 300       | null            |
| 2024-01-02 | 150            | 1               | 225       | 300             |

---

## ✅ Data Quality Checks

* Validación de datasets no vacíos
* Control de valores nulos en métricas clave
* Verificación de consistencia antes de persistencia

---

## 🧠 Decisiones de diseño

* Uso de arquitectura Medallion para separar responsabilidades
* Modularización del código en notebooks y funciones reutilizables
* Uso de Delta Lake para almacenamiento confiable y escalable
* Separación entre lógica de negocio (`transformations`) y utilidades (`utils`)

---

## 🚀 Posibles mejoras

* Orquestación con Databricks Workflows (Jobs)
* Carga incremental (incremental processing)
* Particionado por fecha en tablas Delta
* Integración con herramientas de visualización (Power BI / Tableau)
* Testing automatizado de pipelines

---

## 👨‍💻 Autor

Proyecto desarrollado como práctica de Data Engineering orientada a portfolio.

---
