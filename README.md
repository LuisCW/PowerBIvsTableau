# 📊 Comparativa Power BI vs Tableau

Este documento explica cómo se construyeron las métricas y visualizaciones en **Power BI** y en **Tableau** usando los mismos datos de ventas. También se destacan las diferencias y por qué **Power BI resulta más fácil e intuitivo** en muchos casos.

---

## 🔹 1. KPIs: TotalIngresos y TotalUnidadesVendidas

### Power BI (DAX)
En Power BI usamos **medidas con DAX**:

```DAX
TotalIngresos = SUMX(ventas_techstore, ventas_techstore[cantidad] * ventas_techstore[precio_unitario])

TotalIngresosNetos = [TotalIngresos] - [TotalDescuento]

TotalUnidadesVendidas = SUM(ventas_techstore[cantidad])
