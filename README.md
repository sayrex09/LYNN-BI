# Proyecto Final BI — ANAHUI INDUSTRIAL (Power BI)

Guía de arranque. Sigue los pasos en orden y el tablero funcionará correctamente.

## Archivos de esta carpeta

| Archivo | Qué es | ¿Se usa? |
|---|---|---|
| `LYYN-BI.pbix` | Archivo Power BI **original** | No tocar (respaldo) |
| `ANAHUI_Dataset.xlsx` | **Dataset oficial** (5 tablas, 1.300 ventas) | **SÍ — este** |
| `ANAHUI_Dataset_ORIGINAL_backup.xlsx` | Respaldo del dataset anterior | No (solo respaldo) |
| `CSV_ANAHUI/` | Las 5 tablas en CSV (por si importas suelto) | Alternativa |
| `Tema_ANAHUI_Industrial.json` | Tema de diseño de marca | **SÍ — paso 5** |
| `Guia_Proyecto_BI_ANAHUI.docx` | Guía completa (DAX, EDA, storytelling) | Referencia |
| `RUBRICA Proyecto_Final_BI.docx` | Rúbrica del docente | Referencia |

> Regla de oro: usa siempre **`ANAHUI_Dataset.xlsx`** y trabaja sobre **`LYYN-BI.pbix`**. No edites el original ni el backup.

## Paso 1 — Abrir el proyecto

Abre `LYYN-BI.pbix` con Power BI Desktop (Windows).

## Paso 2 — Cargar / actualizar los datos

Si el archivo ya apunta al Excel, solo pulsa **Inicio (Home) → Actualizar (Refresh)**.

Si tienes que importar desde cero: **Inicio → Obtener datos → Excel**, elige `ANAHUI_Dataset.xlsx`, marca las 5 hojas (FactVentas, DimProducto, DimCliente, DimVendedor, DimTiempo) y **Cargar**.

## Paso 3 — Crear las relaciones (clave para que NO salga estático)

Ve a la **vista Modelo** (icono de tablas, barra izquierda) y arrastra campo sobre campo para crear estas 4 relaciones:

1. `DimTiempo[IDFecha]` → `FactVentas[IDFecha]`
2. `DimProducto[IDProducto]` → `FactVentas[IDProducto]`
3. `DimCliente[IDCliente]` → `FactVentas[IDCliente]`
4. `DimVendedor[IDVendedor]` → `FactVentas[IDVendedor]`

Cada una debe quedar **Uno a varios (1:\*)**, dirección de filtro **Única**, desde la dimensión hacia FactVentas. (Doble clic en la línea para verificar.)

> Si los gráficos muestran el mismo total en todos los meses/años, es porque falta la relación de `IDFecha`. Este paso lo arregla.

## Paso 4 — Marcar la tabla de fechas

Selecciona **DimTiempo → Herramientas de tabla → Marcar como tabla de fechas**, campo `Fecha`. Sin esto, el Crecimiento % y el Acumulado (YTD) salen en blanco.

## Paso 5 — Aplicar el diseño de marca

**Vista (View) → Temas → Buscar temas** y elige `Tema_ANAHUI_Industrial.json`. Reestiliza las 3 páginas con los colores y tarjetas de ANAHUI.

(Ojo: es la pestaña **View**, no **Insert**.)

## Paso 6 — Revisar los ejes

En los gráficos de tendencia usa el campo **`Mes`** de **DimTiempo** en el eje, y ordénalo con **Ordenar por columna → NumMes** para que salga Enero→Diciembre.

## Paso 7 — Verificar

- La línea "Ventas por Mes" varía (pico en marzo, valle en agosto). ✔
- "Ventas por Año" muestra 2024 mayor que 2023 (~+24%). ✔
- Los segmentadores (Año, Categoría, Región) filtran todos los visuales al hacer clic. ✔

Si los tres puntos se cumplen, el tablero está correcto.

## Datos de referencia (dataset actual)

- Ventas totales: S/ 2.254.435 · Margen bruto: 52% · 1.300 transacciones.
- Crecimiento 2024 vs 2023: +23,8%. 2025 es parcial (enero–junio).
- Telas lidera en volumen con el margen más bajo; Prendas y Confección son las más rentables; la región Sur es la de menor venta (oportunidad).

Para el detalle de medidas DAX, EDA y storytelling, abre `Guia_Proyecto_BI_ANAHUI.docx`.
