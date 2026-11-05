# Recordatorio automático de cumpleaños del equipo

**Herramientas:** Power Automate Cloud · Excel Online · Outlook

## Problema
Los cumpleaños del equipo se pasaban por alto o se recordaban a última hora. No había un aviso previo que diera tiempo para organizar un saludo.

## Solución
Un flujo programado que se ejecuta todos los días a primera hora y revisa una tabla de Excel con el nombre, correo y fecha de cumpleaños de cada integrante:

1. **Calcula dos fechas de referencia:** hoy y dentro de 3 días (formato `MM-dd`, para comparar sin importar el año).
2. **Lee la tabla del equipo** en Excel Online.
3. **Convierte la fecha de Excel:** las fechas llegan como número de serie, así que se transforman con `addDays('1899-12-30', ...)`.
4. **Si el cumpleaños es en 3 días:** envía un aviso anticipado al equipo para que preparen un saludo.
5. **Si el cumpleaños es hoy:** envía un recordatorio el mismo día.
6. **Excluye a la persona que cumple años:** el correo se envía a todo el equipo menos a ella, para mantener la sorpresa.

## Técnicas destacadas
- Disparador programado (*Recurrence*) diario.
- Conversión de fechas seriales de Excel a fechas legibles.
- Comparación por mes y día (`MM-dd`) para que funcione todos los años.
- Construcción dinámica de la lista de destinatarios con variables y bucles anidados.

## Resultado
- Ningún cumpleaños pasa desapercibido.
- Aviso con 3 días de anticipación para organizar el saludo.
- Cero mantenimiento: solo se actualiza la tabla cuando entra o sale alguien del equipo.

## Archivos
| Archivo | Descripción |
|---|---|
| `definition.json` | Definición del flujo (Power Automate Cloud) |

> Versión adaptada para portafolio: IDs de archivos, conexiones y datos del equipo fueron reemplazados por marcadores `<...>`. No contiene información personal de nadie.
