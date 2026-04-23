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



# 📊 Sales ETL Pipeline with PySpark on Databricks

## 🚀 Overview

This project implements an end-to-end ETL pipeline using PySpark on Databricks to process sales data, enrich it with product information, and generate aggregated business metrics ready for analysis.

The pipeline follows a **Medallion Architecture (Bronze → Silver → Gold)**, a widely adopted design pattern in modern data engineering.

---

## 🧱 Architecture

```plaintext
Bronze (raw data)
    ↓
Silver (cleaned & enriched data)
    ↓
Gold (business-ready metrics)
```

---

## ⚙️ Tech Stack

* PySpark
* Databricks
* Delta Lake
* SQL

---

## 📂 Project Structure

```plaintext
etl-ventas-databricks/
│
├── notebooks/
│   ├── 01_extract.ipynb
│   ├── 02_transform.ipynb
│   ├── 03_load.ipynb
│
├── src/
│   ├── transformations.ipynb
│   ├── utils.ipynb
│
├── README.md
```

---

## 🔄 ETL Pipeline

### 🥉 1. Extract

* Ingests or generates raw sales and product data
* Stores data in Delta tables within the **bronze layer**

**Output tables:**

* `bronze.ventas_raw`
* `bronze.productos`

---

### 🥈 2. Transform

* Cleans data (filters nulls and invalid values)
* Joins sales data with product information
* Computes key business metrics:

  * Total sales per day
  * Unique customers
  * 7-day moving average (window function)
  * Previous day comparison

**Output:**

* `silver.resumen_diario`

---

### 🥇 3. Load

* Performs data quality validations
* Writes final dataset using Delta Lake
* Produces a business-ready table optimized for analytics

**Final output:**

* `gold.ventas_diarias`

---

## 📈 Sample Output

| date       | total_sales | unique_customers | sales_7d_avg | previous_day_sales |
| ---------- | ----------- | ---------------- | ------------ | ------------------ |
| 2024-01-01 | 300         | 2                | 300          | null               |
| 2024-01-02 | 150         | 1                | 225          | 300                |

---

## ✅ Data Quality Checks

* Validation of non-empty datasets
* Null checks on critical metrics
* Basic consistency validation before persistence

---

## 🧠 Design Decisions

* **Medallion Architecture** to separate data layers and responsibilities
* **Modular design** using reusable transformation and utility functions
* **Delta Lake** for reliable and scalable storage
* Clear separation between business logic (`transformations`) and helper functions (`utils`)

---

## 🚀 Future Improvements

* Pipeline orchestration using Databricks Workflows (Jobs)
* Incremental data processing
* Partitioning strategies for performance optimization
* Integration with BI tools (Power BI / Tableau)
* Automated testing for data pipelines

---

## 👨‍💻 Author

Developed as a hands-on Data Engineering project focused on building production-like pipelines using modern tools and best practices.

---
