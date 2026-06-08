# CLAUDE.md — Proyecto Dashboard LiveHome SPA

## Contexto del negocio

**Empresa:** LiveHome SPA  
**Usuario:** Leslie Escobar (`lescobar@biopure.cl`)  
**Rol:** Gestión financiera / CFO (maneja reportes de ventas, costos de importación, comisiones y P&L)

LiveHome SPA opera con dos líneas de negocio relacionadas: **LiveHome** (productos del hogar) y **Auralis** (productos de cuidado personal). También existe la empresa relacionada **Biopure**.

---

## Objetivo del proyecto

Construir un **dashboard mensual de comisiones** que consolide ventas y comisiones por vendedor. Actualmente existe en dos formatos:

1. **Excel** — `Dashboard Comisiones Mayo 2026.xlsx` en la carpeta del proyecto
2. **HTML interactivo** — publicado en Vercel con diseño dark, animaciones, filtros y gráficos

El dashboard se actualiza **una vez al mes** y lo usa **Leslie exclusivamente**.

---

## Fuentes de datos (Mayo 2026 como modelo)

Todos los archivos están en Google Drive:
```
Mi unidad/REPORTES LIVEHOME SPA/2026/05 MAYO/
```

| Archivo | Contenido |
|---|---|
| `Informe de ventas Livehome Mayo 2026.xlsx` | Comisiones por vendedor (Katy, Pablo, Livehome general) |
| `Costo de Venta mayo 2026.xlsx` | Detalle línea a línea de todas las ventas del mes |
| `Costo de mercadería Mayo 26.xlsx` | Despachos aduaneros: costos en USD y CLP por importación |

La nomenclatura de archivos cambia mes a mes pero sigue el mismo patrón.

### Estructura del informe de ventas
- Hoja por vendedor: `Comisión Katy`, `Livehome comisión`, `Comisión Pablo`
- Columnas clave: Vendedor, Documento, RUT Cliente, Nombre Cliente, Cantidad, Artículo, Venta Neta Real, Consultiva
- Los encabezados reales están en **fila 2** (fila 1 es el período)

### Estructura del costo de venta
- Una sola hoja con ~2.400 filas
- Encabezados reales en **fila 3** (filas 1-2 son período)
- Columnas: Fecha, Nº Documento, Cliente, Cantidad, Producto (código), Descripción, Precio Unitario, Total Neto Línea

### Estructura del costo de mercadería
- Una hoja por despacho aduanero (nombre = número de despacho o proveedor)
- Última hoja (`Hoja1`): tabla de costo unitario por SKU en CLP
- Datos clave: Total USD, Total CLP invoice, Total con gastos de aduana, Honorarios agencia

---

## Archivos de referencia consolidados (nivel anual)

```
Mi unidad/REPORTES LIVEHOME SPA/2026/
├── 2026 P&L LiveHome SPA.xlsx       ← Estado de resultado anual
├── 2026 Auralis P&L.xlsx
├── Costo acumulado 2026.xlsx
├── INVENTARIO 2026.xlsx
├── Conciliacion 2026.xlsx
└── Gastos por centro de negocios 2026.xlsx
```

---

## Convenciones y preferencias

- **Idioma:** Español (Chile) — nombres de hojas, columnas y etiquetas en español
- **Moneda:** CLP como moneda base; USD solo en contexto de importaciones
- **Formato fechas:** DD-MM-YYYY
- **Números negativos:** Paréntesis, ej. `(1.234)`
- **Separador miles:** Punto `.` | Separador decimal: Coma `,` (estándar chileno)
- **Cero:** Mostrar como `-`

---

## Guía para construir el dashboard

### Diseño sugerido (a validar con Leslie)
- **Hoja `Dashboard`** — vista resumen con KPIs del mes y gráficos
- **Hoja `Ventas`** — tabla dinámica consolidada desde el informe de ventas
- **Hoja `Comisiones`** — resumen por vendedor con total comisión calculada
- **Hoja `Costos Import.`** — resumen de despachos del mes
- **Hojas de datos** — datos crudos importados (no modificar manualmente)

### KPIs prioritarios (ventas)
1. Venta neta total del mes
2. Venta neta por vendedor
3. Productos más vendidos (top 5)
4. Número de clientes únicos
5. Comisión total a pagar por vendedor

### Estilo visual
- Fuente: Arial o Calibri
- Color principal: azul corporativo
- Usar tablas de Excel (`Ctrl+T`) para facilitar actualización mensual
- Sin fórmulas hardcodeadas — todo debe recalcular al reemplazar los datos fuente

---

## Lo que NO hacer

- No modificar los archivos fuente originales
- No usar macros VBA (Leslie no los activa)
- No crear fórmulas que dependan de rutas absolutas de Google Drive (se rompen entre equipos)
- No agregar columnas de cálculo dentro de las hojas de datos crudos

---

## Estado actual (Junio 2026)

- [x] Dashboard HTML publicado en Vercel con clave `livehome2026`
- [x] Repositorio GitHub creado: `lescobar-great/dashboard-comisiones-livehome`
- [x] Vercel conectado a GitHub — cada `git push` despliega automáticamente
- [x] Dashboard Excel creado en la carpeta del proyecto
- [ ] Evaluar agregar costos e importaciones en una segunda fase
- [ ] Actualizar dashboard con datos de Junio 2026

---

## URLs y accesos

| Recurso | URL |
|---|---|
| Dashboard publicado | https://dashboard-comisiones-livehome.vercel.app |
| Repositorio GitHub | https://github.com/lescobar-great/dashboard-comisiones-livehome |
| Clave dashboard | `livehome2026` |

---

## Cómo actualizar el dashboard cada mes

1. Copiar los nuevos archivos `.xlsx` a la carpeta de mayo correspondiente en Google Drive
2. Actualizar los datos en `index.html` (valores de KPIs, tabla y desglose)
3. Ejecutar `/sync` — Claude hace commit, push y Vercel despliega automáticamente

---

## Próximos pasos

- [ ] Actualizar dashboard con datos de Junio 2026
- [ ] Evaluar agregar costos e importaciones en una segunda fase
