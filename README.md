# 🚀 RappiPlus: De Datos a Decisiones de Negocio

Análisis end-to-end del desempeño de RappiPlus, un servicio de suscripción dentro del ecosistema Rappi diseñado para aumentar frecuencia de compra y valor por usuario. El proyecto responde, con evidencia de datos, si el servicio realmente cumple su objetivo — cubriendo calidad de datos, rentabilidad, funnel de conversión, retención por cohortes, validación estadística de un experimento y comunicación ejecutiva en dashboard.

🔗 **[Ver dashboard interactivo en Power BI Service](https://app.powerbi.com/view?r=eyJrIjoiYmQ1MWMzZTQtMWFlOC00MjZmLWIwMDEtODlkNzJiMDY5MmI4IiwidCI6IjI2NGEzYzA5LWUzOGQtNDdlZi04NzE0LWY3YzEwZGZiOThjZSIsImMiOjR9)**

## 🎯 Contexto de negocio

El equipo de negocio de RappiPlus tenía dudas concretas sin responder: ¿los usuarios suscritos realmente compran más?, ¿el modelo genera ganancias?, ¿dónde se pierden oportunidades en el proceso de compra?, ¿los usuarios regresan?, y ¿los cambios de producto generan impacto medible? El proyecto sigue una lógica progresiva de 6 etapas, cada una construida sobre la anterior.

## 🧱 Datos

Cinco fuentes: `rappiplus_orders_raw.csv` (pedidos, precios, descuentos, revenue), `rappiplus_catalog.csv` (costos y proveedores), `rappiplus_marketing_spend.csv` (inversión por canal/país), tablas SQL `events`/`users`/`user_activity` (comportamiento del usuario) y `experiment_checkout_ui.csv` (resultados de un experimento A/B en checkout).

## 🧮 Metodología — 6 etapas

**1. Calidad de datos (Python).** Sobre 25,100 pedidos: auditoría de devoluciones, valores inconsistentes y duplicados, dejando el dataset validado con banderas de auditoría en vez de eliminar registros "sospechosos" sin evidencia.

**2. Rentabilidad (KPIs de negocio).** Cálculo de revenue, costos y profit — con el hallazgo crítico del proyecto (ver abajo).

**3. Funnel de conversión (SQL).** Construcción del embudo completo con SQL avanzado (CTEs, funciones de ventana) sobre la tabla `events`.

**4. Retención por cohortes (SQL).** Retención semanal por cohorte mensual de registro.

**5. Test estadístico (Python).** Validación de un rediseño de checkout con prueba de hipótesis formal.

**6. Comunicación (Power BI).** Consolidación de los 3 CSVs limpios en un dashboard ejecutivo publicado en Power BI Service.

## 🔎 Hallazgo crítico — Calidad de datos que cambia la decisión

**10 pedidos (0.04% del dataset)** con cantidades no plausibles (10,000–20,000 unidades) distorsionaban el margen reportado del negocio: **11.5%** con esos registros incluidos vs. **30.5% real** una vez excluidos y validados. Es el hallazgo más importante de todo el proyecto — sin esta auditoría, el equipo de negocio habría tomado decisiones de pricing o inversión basadas en una rentabilidad subestimada en más de la mitad de su valor real.

*Recomendación:* confirmar estos 10 registros con el equipo de operaciones antes de reportarlos como rentabilidad oficial — podrían ser errores de captura o casos legítimos de compra corporativa que requieren tratamiento contable distinto.

## 📊 Resultados por etapa

**Funnel de conversión:** 7,796 usuarios únicos en `first_visit`, conversión total del **80%** hasta `purchase`. Se detectó una anomalía en la etapa `add_to_cart` (conversión superior al 100%), documentada explícitamente como hallazgo a validar con el equipo de producto — no como error propio de cálculo.

**Retención por cohortes:** estabilidad de 40-44% en las semanas 1 a 3 post-registro, sin señales de fuga crítica entre cohortes mensuales.

**Test A/B (rediseño de checkout):** prueba Z de dos proporciones — resultado **no estadísticamente significativo** (p = 0.4161). El cambio de UI no demostró impacto medible en conversión, y se reportó así en vez de forzar una conclusión positiva.

## 📁 Estructura del repositorio

```
rappiplus-datos-a-decisiones/
├── README.md
├── notebook/
│   └── rappiplus_analisis_completo.ipynb
├── sql/
│   ├── funnel_conversion.sql
│   └── retencion_cohortes.sql
├── dashboard/
│   └── PROYECTO_RAPPI_PLUS.pbix
└── data/
    ├── orders_clean.csv
    ├── catalog_clean.csv
    └── marketing_clean.csv
```

## 🛠️ Herramientas

Python (Pandas, auditoría de calidad de datos, pruebas de hipótesis con SciPy) — SQL (CTEs, funciones de ventana, funnel y cohortes) — Power BI (modelado, dashboard ejecutivo, Power BI Service).
