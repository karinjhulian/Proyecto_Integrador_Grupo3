# 📊 Solución de BI para evaluar la inversión en descuentos promocionales

**Proyecto Integrador · Grupo 3 · Licenciatura en Ingeniería de Ciencia de Datos e Inteligencia de Negocios · UNIVALLE**

![SQL Server](https://img.shields.io/badge/SQL%20Server-2014-CC2927?logo=microsoftsqlserver&logoColor=white)
![SSIS](https://img.shields.io/badge/ETL-SSIS-5C2D91?logo=visualstudio&logoColor=white)
![R](https://img.shields.io/badge/R-R%20Markdown-276DC3?logo=r&logoColor=white)
![Estado](https://img.shields.io/badge/avance-Fases%201%20a%203-2C5F8A)

> ¿Las campañas promocionales de un e-commerce generan suficientes ventas para compensar el ingreso que se cede en descuentos? Este proyecto lo responde con un **data warehouse**, **análisis estadístico** y un **modelo de regresión** sobre las ventas de 2016 a 2022.

---

## 👥 Equipo

| Integrante |
|---|
| Rocha Gonzales, Karin Jhulian |
| Torrez Raña, Sebastián |
| Lecoña Chavez, Camila Milagros |

**Docente:** Lic. Carol Osinaga

---

## 🎯 Objetivo

Determinar, mediante una solución de Business Intelligence basada en el data warehouse **MarketingDW**, si las campañas promocionales aplicadas entre 2016 y 2022 generaron un aumento de ventas suficiente para compensar los ingresos cedidos en descuentos, y definir la asignación de campañas, categorías y niveles de descuento que maximice el **ingreso neto**.

---

## 🔎 Hallazgos principales

| Indicador | Resultado |
|---|---|
| Órdenes analizadas | 50,000 (274,566 líneas de venta) |
| Descuento cedido | 32.8 millones (4.2 % del ingreso bruto) |
| Aumento de ventas necesario para compensar el descuento | **+17.5 %** |
| Aumento observado del ingreso bruto por orden con campaña | **−0.9 %** (no significativo) |
| Efecto del descuento sobre las unidades vendidas | ≈ 0 (elasticidad 0.0055, *p* = .330) |
| Ingreso neto adicional estimado sin descuentos | **+32.9 millones** |

**Conclusión:** las campañas no aumentan las ventas, así que el descuento se traduce directamente en ingreso cedido.

---

## 🗂️ Estructura del repositorio

```
Proyecto_Integrador_Grupo3/
├── 02_Fase2_DataWarehouse/
│   ├── Proyecto_SSIS_VisualStudio.zip    → paquete ETL (SSIS)
│   └── Bases_SQLServer.zip               → respaldos .bak de MarketingOLTP y MarketingDW
├── 03_Fase3/
│   ├── 3.1_Estadistica/                  → análisis estadístico (.Rmd + .html)
│   └── 3.2_Modelizacion/                 → modelo de regresión (.Rmd + .html)
└── 04_Informes/
    └── Informe_Proyecto_Integrador_Fases_1_a_3   → informe en formato APA
```

> 💡 Los archivos `.html` se pueden abrir directamente en el navegador para ver los resultados sin instalar nada.

---

## 🧭 Fases del proyecto

| Fase | Materia | Contenido | Estado |
|:---:|---|---|:---:|
| 1 | Proyecto Integrador I | Problema, objetivos SMART, requerimientos de información y KPIs | ✅ |
| 2 | Data Warehousing | Modelo estrella y carga ETL con SSIS | ✅ |
| 3 | Métodos y Programas Estadísticos IV | Exploratorio, relaciones y patrones, pruebas de hipótesis, supervivencia | ✅ |
| 3 | Modelización Empresarial I | Regresión múltiple por MCO, modelo log-log y escenarios de descuento | ✅ |
| 4 | Dirección Financiera y Dirección de Marketing | Impacto financiero y segmentación | ⏳ |
| 5 | Optimización Empresarial I | Asignación óptima de descuentos | ⏳ |
| 6 | Integración BI | Tablero de KPIs y recomendaciones | ⏳ |

---

## 🏗️ Modelo de datos

Esquema en estrella con una tabla de hechos y seis dimensiones:

```
                DIM_TIEMPO
                    │
DIM_CLIENTE ── FACT_VENTAS ── DIM_PRODUCTO
               │    │    │
   DIM_PROVEEDOR    │    DIM_METODO_PAGO
                DIM_CAMPAÑA
```

**Grano:** una fila por línea de orden.

---

## ▶️ Cómo reproducir los resultados

1. **Restaurar las bases:** descomprime `Bases_SQLServer.zip` y restaura `MarketingOLTP.bak` y `MarketingDW.bak` en SQL Server (SSMS → *Bases de datos* → *Restaurar base de datos*).
2. **Instalar los paquetes de R** (en RStudio):
   ```r
   options(repos = c(CRAN = "https://packagemanager.posit.co/cran/2022-04-01"))
   install.packages(c("dplyr", "tidyr", "ggplot2", "lubridate", "scales", "broom", "survival",
                      "knitr", "rmarkdown", "lmtest", "sandwich", "DBI", "odbc"))
   ```
3. **Configurar el servidor:** en cada `.Rmd`, cambia el nombre del servidor en el bloque de conexión:
   ```r
   servidor <- "NOMBRE_DE_TU_SERVIDOR"
   ```
4. **Compilar:** abre el `.Rmd` y presiona **Knit**.

> Para revisar el ETL, descomprime `Proyecto_SSIS_VisualStudio.zip` y abre la solución `.sln` en Visual Studio con SQL Server Integration Services.

---

## 📚 Fuente de datos

Conjunto de datos **OLTP: Ecommerce data**, publicado en Kaggle: [enlace al dataset](PEGAR_AQUÍ_EL_LINK_DE_KAGGLE).
Los datos se usan con fines académicos, según la licencia indicada en su página.

---

<p align="center"><i>Universidad Privada del Valle · Santa Cruz de la Sierra, Bolivia · 2026</i></p>
