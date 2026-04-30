#   Online Retail II UCI
Context
This Online Retail II data set contains all the transactions occurring for a UK-based and registered, non-store online retail between 01/12/2009 and 09/12/2011.The company mainly sells unique all-occasion gift-ware. Many customers of the company are wholesalers.

# Análisis de Ventas Retail — Decision Intelligence

> Proyecto de análisis exploratorio y segmentación de clientes para una empresa retail, orientado a decisiones de negocio accionables.

---

## Problema de negocio

La empresa tiene datos de transacciones pero carece de visibilidad sobre:
- ¿Qué meses son buenos o malos y por qué?
- ¿Qué productos impulsan el revenue y cuáles se deben descontinuar?
- ¿Qué clientes merecen mayor inversión en retención?

---

## Stack tecnológico

| Capa | Herramienta |
|------|-------------|
| Lenguaje | Python 3.10 |
| Manipulación | pandas, numpy |
| Visualización | matplotlib, seaborn |
| Dashboard | Power BI / Tableau |
| Dataset | Online Retail II — UCI / Kaggle |

---

## Estructura del repositorio

```
retail-sales-analysis/
├── data/
│   └── online_retail_II.csv          # Dataset fuente (no incluido en repo)
├── notebooks/
│   └── retail_analysis.ipynb         # Análisis completo comentado
├── outputs/
│   ├── rfm_segments.csv              # Segmentos RFM exportados
│   ├── top_products.csv              # Ranking de productos
│   ├── monthly_trend.csv             # Tendencia mensual
│   ├── 01_monthly_trend.png          # Gráfica de tendencia
│   ├── 02_top_products.png           # Top productos
│   └── 03_rfm_segments.png          # Distribución RFM
├── dashboard/
│   └── retail_dashboard.pbix         # Dashboard Power BI
└── README.md
```

---

## Análisis realizado

### KPIs calculados
- Revenue total, órdenes únicas, ticket promedio, clientes únicos
- Comparativa año vs año

### Tendencias
- Revenue mensual con detección de estacionalidad
- Identificación de meses fuertes (Nov-Dic) y valles (Feb-Mar)

### Productos
- Top 15 SKUs por revenue acumulado
- Productos con baja rotación (menos de 5 unidades en 90 días)
- Proporción del catálogo activo vs inactivo

### Segmentación RFM
Cada cliente recibe un score de Recencia, Frecuencia y Monetario (escala 1-5) y es clasificado en:

| Segmento | Criterio | % típico de clientes |
|----------|----------|----------------------|
| Champions | R≥4, F≥4, M≥4 | ~16% |
| Leales | R≥3, F≥3 | ~21% |
| Potenciales | R≥4, F≤2 | ~15% |
| En riesgo | R=2 | ~12% |
| Hibernando | R=1, F<3 | ~22% |
| No puedo perderlos | R=1, F≥3 | ~14% |

---

## Hallazgos principales

1. **Estacionalidad**: Nov-Dic concentran ~28% del revenue. El Q1 es consistentemente el más débil.
2. **Pareto de productos**: El top 20% de SKUs genera el 80% del revenue.
3. **Stock muerto**: ~18% del catálogo sin movimiento en los últimos 90 días.
4. **Champions + Leales**: 37% de clientes → 65% del revenue.
5. **Clientes en riesgo**: 630 cuentas con señales de churn que aún tienen valor rescatable.

---

## Recomendaciones de negocio

### Corto plazo (0-30 días)
- Lanzar campaña **win-back** para segmento "En riesgo" (descuento 15%, asunto personalizado)
- Liquidar o crear bundles con los 20 SKUs de menor rotación

### Mediano plazo (30-90 días)
- Implementar **programa de lealtad** para Champions y Leales (early access, envío gratis)
- Planificar inventario para temporada alta con 8 semanas de anticipación

### Largo plazo
- Automatizar el recálculo mensual de RFM con un job de Python + cron
- Integrar el dashboard con datos en tiempo real vía API del POS

---

## Cómo reproducir

```bash
# 1. Clonar el repositorio
git clone https://github.com/tu-usuario/retail-sales-analysis.git
cd retail-sales-analysis

# 2. Instalar dependencias
pip install pandas numpy matplotlib seaborn jupyter

# 3. Descargar el dataset
# https://www.kaggle.com/datasets/mashlyn/online-retail-ii-uci
# Guardar como: data/online_retail_II.csv

# 4. Ejecutar el notebook
jupyter notebook notebooks/retail_analysis.ipynb
```

---

## Dataset

**Online Retail II** — UCI Machine Learning Repository  
Transacciones de un retailer de UK (2009-2011) con ~1M filas  
Columnas: `Invoice`, `StockCode`, `Description`, `Quantity`, `InvoiceDate`, `Price`, `Customer ID`, `Country`

---
