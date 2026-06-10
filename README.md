# GEB — Gestión de Equipos Biomédicos Críticos · HRT 2026

Aplicación de **un solo archivo HTML** (`index.html`) para administrar el
programa de mantenciones preventivas (PMP), las mantenciones correctivas /
servicio técnico y los pendientes de los equipos críticos del Hospital
Regional de Temuco. No necesita internet, servidor ni instalación.

## Cómo empezar

1. Descarga `index.html` y guárdalo en tu computador (o carpeta de red).
2. Ábrelo con doble clic (Chrome o Edge).
3. La aplicación parte **vacía**: importa el Excel maestro
   **Programación MP (.xlsm)** desde el botón del Panel (o en la pestaña
   Datos). Se cargan el inventario y el plan anual; todo lo demás
   —fichas, correctivos, pendientes, asignaciones— lo registras tú en el
   día a día.

Todos los cambios se guardan automáticamente en el navegador
(localStorage). En la pestaña **Datos** puedes exportar un respaldo `.json`
(recomendado cada semana) e importarlo en otro computador.

## Importación del Excel maestro

Se leen las hojas `PMP_2026` (programación X / R / RA / PM) y
`Registro_MP-2026` (resultados Si, Si-RA, C1–C8, FS, No, NU, Baja),
columnas B–AE **excluyendo Q (Observación) y S (Responsable MP)**. La
fusión no borra nada registrado en la aplicación: si reimportas un archivo
actualizado, se refrescan inventario, plan y resultados, se agregan los
equipos con ID nuevo, y se conserva todo lo tuyo (incluido el resultado de
un mes que el archivo traiga vacío). El lector de Excel está integrado en
la página (sin librerías externas) y funciona sin internet.

## Qué resuelve

| Dolor | Dónde lo resuelve |
|---|---|
| No sé cuántas MP van realizadas, pendientes y de quién | **Panel** (KPIs, cumplimiento mensual, tabla por responsable) |
| Equipos meses en servicio técnico sin trazabilidad | **Correctivos / ST**: hitos del proceso (folio SIGEM, OC, envío, retorno) + días en cada estado |
| "Le pregunté a Ignacio pero no tengo registro" | Bitácora de **seguimiento** por caso, con fecha |
| Pendientes en la cabeza o libreta | **Pendientes** con fecha límite, subtareas y actualizaciones |
| Plazos de 30 días de las causales C1/C5–C8 | Alertas automáticas de vencimiento y aviso de retiro de circulación (FS) |
| Informe de empresa externa que nadie vuelve a pedir | Checklist documental por MP externa + alerta a los 15 días |
| Generar el Excel de asignación mensual | **Asignación mensual**: ejecutores, exportación CSV e impresión |
| Ficha técnica en papel | Historial cronológico por equipo, alimentado automáticamente, imprimible |
