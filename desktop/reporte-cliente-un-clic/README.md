# Reporte de cliente automatizado con envío en un clic

**Herramienta:** Power Automate Desktop · Excel (VBA) · Outlook · Power BI Report Server

## Problema
Cada vez que se necesitaba el reporte de un cliente, había que entrar al dashboard de Power BI, filtrar el cliente y el tipo de contenedor, exportar los datos, procesarlos en Excel y armar el correo a mano. Era una tarea repetitiva y propensa a errores.

## Solución
Un flujo de Power Automate Desktop que hace todo el proceso con un solo clic:

1. Abre el dashboard de volumen en Power BI Report Server (Edge).
2. Selecciona la pestaña del cliente y filtra el tipo de contenedor (*Dry*).
3. Muestra el visual como tabla y exporta los datos a Excel.
4. Toma automáticamente el archivo más reciente de la carpeta de Descargas.
5. Abre la plantilla `.xlsm` y ejecuta la macro VBA `ProcesarReporte`, que procesa los datos exportados.
6. Guarda y cierra el Excel.
7. Envía el reporte por Outlook con un correo HTML con formato y la fecha del día en el asunto.

## Resultado
- El reporte pasa de un proceso manual de varios pasos a **un solo clic**.
- [Agrega aquí el tiempo ahorrado, por ejemplo: de ~X minutos a menos de 1 minuto por envío.]
- Formato de correo estandarizado y sin errores de copiado.

## Archivos
| Archivo | Descripción |
|---|---|
| `flujo.txt` | Código del flujo (lenguaje de Power Automate Desktop) |


## Cómo usarlo
1. Abre Power Automate Desktop y crea un flujo nuevo.
2. Copia el contenido de `flujo.txt` y pégalo en el diseñador (Ctrl + V).
3. Reemplaza los marcadores `<...>` (servidor, usuario, correos) por tus datos.
4. Vuelve a capturar los elementos de la página web, ya que esta versión pública no incluye los selectores de UI.

> Versión adaptada para portafolio: no contiene servidores, correos ni datos reales de ninguna empresa.
