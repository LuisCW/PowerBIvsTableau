# 📊 Comparativa Power BI vs Tableau

Este documento explica cómo se construyeron las métricas y visualizaciones en **Power BI** y en **Tableau** usando los mismos datos de ventas. También se destacan las diferencias y por qué **Power BI resulta más fácil e intuitivo** en muchos casos.

---

## 🔹 1. KPIs: TotalIngresos y TotalUnidadesVendidas

### Power BI (DAX)
```DAX
TotalIngresos = SUMX(ventas_techstore, ventas_techstore[cantidad] * ventas_techstore[precio_unitario])

TotalIngresosNetos = [TotalIngresos] - [TotalDescuento]

TotalUnidadesVendidas = SUM(ventas_techstore[cantidad])
```

✅ Muy directo, se crean en el **panel de medidas**.  
✅ Una vez creadas, pueden reutilizarse en cualquier gráfico o tarjeta KPI.  
✅ DAX permite manejar fácilmente cálculos de fila y agregaciones.

---

### Tableau (Calculated Fields)
```tableau
// Total de ingresos
SUM([cantidad] * [precio_unitario])

// Total ingresos netos
SUM([cantidad] * [precio_unitario]) - SUM([descuento])

// Total unidades vendidas
SUM([cantidad])
```

⚠️ Cada cálculo debe hacerse como un **campo calculado** y luego arrastrarse a la vista.  
⚠️ Si no se define bien el contexto, Tableau puede sumar por nivel de detalle distinto al esperado.  
⚠️ Requiere ajustar agregaciones manualmente (`SUM`, `AVG`, etc.).

---

## 🔹 2. Top 10 productos más vendidos

### Power BI
- Se agrega un gráfico de barras.  
- En el panel de filtros → **"Mostrar los 10 primeros"** en base a `[TotalIngresos]` o `[TotalUnidadesVendidas]`.  
- Con 2 clics queda filtrado.  

✅ Muy intuitivo con la opción de **Top N** en filtros visuales.

---

### Tableau
- Crear un gráfico de barras con `[nombre_producto]` y `[TotalIngresos]`.  
- Clic derecho en `[nombre_producto]` → **Filtro** → pestaña **Top** → elegir "Por campo" → **Top 10 por SUM([TotalIngresos])**.  

⚠️ El proceso es menos evidente y requiere más pasos que en Power BI.  
⚠️ Hay que entender bien los filtros de Tableau (Dimensión vs Medida) para que funcione.

---

## 🔹 3. Ventas por categoría

### Power BI
- Crear un gráfico de pastel o barras.  
- Colocar `[categoría]` en el eje y `[TotalIngresos]` en valores.  
- Listo, en segundos se visualiza.

### Tableau
- Colocar `[categoría]` en columnas y `[SUM(TotalIngresos)]` en filas.  
- Cambiar a gráfico circular desde "Show Me".  
- Arrastrar `[categoría]` a color.  

⚠️ Tableau requiere más arrastres y configuraciones iniciales.  

---

## 🔹 4. Performance de vendedores

### Power BI
- Tabla con `[vendedor]` y medidas: `[TotalIngresosNetos]`, `[TotalUnidadesVendidas]`, `[TicketPromedio]`.  
- Ranking con función `RANKX`.

### Tableau
- Tabla cruzada (`Text Table`) con `[vendedor]` en filas.  
- Campos calculados para TicketPromedio y ranking manual con `INDEX()`.  

⚠️ En Tableau hay que crear cálculos adicionales para el ranking.  
⚠️ En Power BI, DAX lo resuelve de forma más limpia.

---

## 🎯 Conclusión

- **Power BI** es **más fácil e intuitivo** para usuarios de negocio:  
  - Filtros "Top N" listos.  
  - DAX aunque potente, es fácil de aplicar en medidas simples.  
  - Visualizaciones más rápidas de configurar.  

- **Tableau** es más flexible y poderoso para análisis avanzados:  
  - Control detallado del nivel de detalle (LOD).  
  - Más opciones de visualización.  
  - Pero requiere mayor curva de aprendizaje.  

👉 Para **dashboards rápidos de ventas y KPIs**, **Power BI** suele ser más eficiente.  
👉 Para **análisis exploratorios profundos**, **Tableau** ofrece más control.

---

TotalUnidadesVendidas = SUM(ventas_techstore[cantidad])
