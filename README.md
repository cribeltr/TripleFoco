# GEB — Gestión de Equipos Biomédicos Críticos · HRT 2026

Aplicación de **un solo archivo HTML** para administrar el programa de
mantenciones preventivas (PMP), las mantenciones correctivas / servicio
técnico y los pendientes de los 966 equipos críticos del Hospital Regional
de Temuco. No necesita internet, servidor ni instalación.

## Cómo usarla

1. Descarga `index.html` y guárdalo en tu computador (o carpeta de red).
2. Ábrelo con doble clic (Chrome o Edge).
3. Listo: ya viene cargado con el inventario, el plan anual y los
   resultados del maestro `Programación MP 2026.xlsm`.

Todos los cambios se guardan automáticamente en el navegador
(localStorage). En la pestaña **Datos** puedes exportar un respaldo `.json`
(recomendado cada semana) e importarlo en otro computador.

## Qué resuelve

| Dolor actual | Dónde lo resuelve |
|---|---|
| No sé cuántas MP van realizadas, pendientes y de quién | **Panel** (KPIs, cumplimiento mensual, tabla "por cobrar" por responsable) |
| Equipos meses en servicio técnico sin trazabilidad | **Correctivos / ST**: hitos del proceso (folio SIGEM, OC, envío, retorno) + días en cada estado |
| "Le pregunté a Ignacio pero no tengo registro" | Bitácora de **seguimiento** por caso, con fecha |
| Pendientes en la cabeza o libreta | **Pendientes** con fecha límite, subtareas y actualizaciones |
| Plazos de 30 días de las causales C1/C5–C8 | Alertas automáticas de vencimiento y aviso de retiro de circulación (FS) |
| Informe de empresa externa que nadie vuelve a pedir | Checklist documental por MP externa + alerta a los 15 días |
| Generar el Excel de asignación mensual | **Asignación mensual**: responsables, exportación CSV e impresión |
| Ficha técnica en papel | Historial cronológico por equipo, alimentado automáticamente, imprimible |

## Mantenimiento

- `plantilla.html` es el código fuente de la app (con marcador `__DATA__`).
- `herramientas/generar.py` regenera `index.html` desde el Excel maestro:

```bash
pip install openpyxl
python3 herramientas/generar.py "Programación MP 2026.xlsm"
```

Útil para partir un año nuevo. Antes de restablecer datos en la app,
exporta un respaldo desde la pestaña **Datos**.
