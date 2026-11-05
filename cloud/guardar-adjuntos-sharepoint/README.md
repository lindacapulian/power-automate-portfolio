# Guardado automático del reporte diario en SharePoint

**Herramientas:** Power Automate Cloud · Outlook · SharePoint

## Problema
La plataforma de contact center envía todos los días por correo un reporte con el tiempo de conexión de los agentes. Había que descargar el adjunto, renombrarlo y guardarlo a mano en SharePoint para que el dashboard de Power BI lo pudiera leer. Si alguien lo olvidaba, el dashboard quedaba desactualizado.

## Solución
Un flujo que se activa solo cuando llega el correo y deja el archivo listo en SharePoint:

1. **Detecta el correo correcto:** se activa al llegar un mensaje del remitente del reporte, con el asunto esperado y con archivo adjunto.
2. **Recorre los adjuntos** del correo.
3. **Filtra el archivo correcto:** solo procesa los adjuntos cuyo nombre empieza con `REPORTE_DIARIO_`.
4. **Lo guarda en SharePoint** con un nombre estandarizado por fecha: `LOGIN_yyyy-MM-dd.xlsx`, usando la fecha del día anterior, que es el día que reporta.

## Técnicas destacadas
- Disparador por evento (*When a new email arrives*) con filtros de remitente, asunto y adjuntos.
- Bucles anidados para recorrer correos y adjuntos.
- Conversión del adjunto con `base64ToBinary()`.
- Nomenclatura dinámica con `formatDateTime(addDays(utcNow(), -1), 'yyyy-MM-dd')`.
- Transferencia por bloques (*chunked*) para archivos grandes.

## Resultado
- El histórico diario se arma solo, sin intervención manual.
- Archivos con nombres consistentes, listos para que Power Query los combine en el dashboard.
- Se elimina el riesgo de días faltantes por olvido.

## Archivos
| Archivo | Descripción |
|---|---|
| `definition.json` | Definición del flujo (Power Automate Cloud) |

> Versión adaptada para portafolio: sitio de SharePoint, rutas, remitente y conexiones fueron reemplazados por marcadores `<...>`. No contiene datos reales de ninguna empresa.
