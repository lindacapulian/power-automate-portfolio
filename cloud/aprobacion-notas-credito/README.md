# Aprobación semanal de Notas de Crédito

**Herramientas:** Power Automate Cloud · SharePoint · Excel Online · Office Scripts · Outlook

## Problema
Cada semana había que reunir las notas de crédito revisadas, calcular los totales (facturas, notas de crédito, nuevas facturas y monto neto), armar tablas con los casos, agregar el acumulado del año (YTD) y enviar todo por correo para aprobación. Era un proceso manual, largo y con riesgo de errores en los montos.

## Solución
Un flujo de Power Automate Cloud que se ejecuta con un clic desde SharePoint y arma el correo de aprobación completo:

1. **Busca la semana más reciente:** lee la biblioteca de SharePoint, filtra las carpetas `WK xx` y toma la última.
2. **Lee el Excel de la semana:** obtiene las filas de la tabla de casos y descarta las que tienen observaciones.
3. **Normaliza los montos:** limpia formatos mixtos (`S/`, `$`, comas y puntos decimales) y calcula el **monto real de la NC** (nota de crédito menos nueva factura).
4. **Calcula totales:** facturas, notas de crédito, nuevas facturas, monto neto y un subtotal de casos *Reactive / Non storage*.
5. **Agrega secciones adicionales** si hay datos: resoluciones finales de OSITRAN y transacciones extrajudiciales (en dólares y soles), cada una con su total.
6. **Genera el resumen YTD:** ejecuta un **Office Script** sobre el archivo acumulado del año, que devuelve una tabla HTML agrupada por tipo de incidente y tipo de factura.
7. **Crea enlaces de solo lectura** al Excel de la semana y al archivo YTD.
8. **Envía el correo de aprobación** con asunto automático (`WK xx.2026 - Credit Notes Approval`), totales, tablas con formato y enlaces.

## Técnicas destacadas
- Selección dinámica de la última carpeta semanal con `Filter array`, `Select` y `sort()`.
- Limpieza de montos con expresiones (`replace`, `coalesce`, `float`) para soportar distintos formatos numéricos.
- Suma de arreglos sin bucles usando `xpath(xml(json(...)), 'sum(...)')`.
- Tablas HTML con estilos y fila de **Grand Total** insertada mediante `replace()`.
- Integración con **Office Scripts** para cálculos que Power Automate no resuelve fácilmente.

## Resultado
- El correo semanal de aprobación se genera completo en **un clic**.
- [Agrega aquí el tiempo ahorrado, por ejemplo: de ~X horas a minutos por semana.]
- Montos calculados de forma consistente, sin errores de digitación.

## Archivos
| Archivo | Descripción |
|---|---|
| `definition.json` | Definición del flujo (Power Automate Cloud) |

> Versión adaptada para portafolio: sitios de SharePoint, IDs, correos y conexiones fueron reemplazados por marcadores `<...>`. No contiene datos reales de ninguna empresa.
