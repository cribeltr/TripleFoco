# CLAUDE.md — Contexto del proyecto GEB

> **Lee este archivo completo antes de tocar código.** Resume meses de trabajo
> iterativo con el usuario y las decisiones que NO deben revertirse.

## Quién es el usuario y para qué existe esto

El usuario es el **ingeniero responsable administrativo de los ~966 equipos
biomédicos críticos del Hospital Regional de Temuco (HHHA)**: incubadoras,
ventiladores, máquinas de anestesia y diálisis, monitores, desfibriladores,
DEA y oxímetros. Sus obligaciones:

1. **Programa anual de mantenciones preventivas (PMP)**: el documento oficial
   por resolución es un Excel (`Programación MP 2026.xlsm`, hojas `PMP_2026`
   y `Registro_MP-2026`). Códigos de plan: X (programada), R (reprogramada),
   RA (reprog. año anterior), PM (puesta en marcha). Resultados: Si, Si-RA,
   C1–C8 (causales de reprogramación), FS, No, NU, Baja.
2. **Causales C1, C5–C8**: plazo máximo 30 días corridos tras el fin del mes
   programado; si vence, corresponde retiro de circulación (FS). C2/C3/C4
   (equipo en ST / espera repuestos / préstamo) no tienen plazo fijo, pero la
   MP debe ejecutarse de inmediato al retorno del equipo.
3. **Familias externas** (Ventiladores, Máquina de Diálisis, M Anestesia): las
   ejecuta una empresa; exigen reporte interno + informe de la empresa.
4. **Correctivos**: flujo folio SIGEM → asignación → compra/OC → envío a
   servicio técnico → visita → retorno → entrega. Él no repara: **delega y
   debe asegurar que se cumpla** (perseguir casos estancados, con registro
   fechado de a quién preguntó y qué respondió).
5. **Carpeta física por equipo**: para "cerrar el mes" no puede faltar ningún
   documento firmado (reporte de reprogramación firmado por la supervisora
   del servicio clínico, protocolos, informes de empresa). Este es el corazón
   de la pestaña **Documentos**.
6. Envía **informes mensuales a cada servicio clínico** y responde a jefatura
   "cuántos en ST / no operativos / % cumplimiento".

## Contrato de trabajo con el usuario (IMPORTANTE)

- **No cuestionar el porqué; preguntar el "¿para qué?"** cuando pida algo y el
  fin no sea evidente, y diseñar la mejor solución para ese fin (no la
  petición literal). Ejemplo real: pidió "anotar pendientes"; el fin era
  "ningún documento sin firmar en la carpeta física" → la solución correcta
  fue el flujo documental automático, no una lista de tareas.
- Busca un programa **minimalista**: prefiere filtrar sobre anotar, y quiere
  podar vistas que no use. La matriz Eisenhower/sapo le generó fatiga visual
  (Pendientes abre en vista lista por decisión suya).
- Responder SIEMPRE en español. Probar con sus respaldos reales antes de
  entregar. Tras cada cambio: commit + push + enviarle `index.html`.
- **Él nutre, Claude razona.** El usuario entrega ideas y ejemplos de cómo lo
  haría a mano ("en Excel yo haría…"): eso es modelo mental para entender la
  lógica, NO un encargo literal. La solución se propone DENTRO de GEB; no
  generar entregables paralelos (planillas externas) cuando lo pedido debe
  vivir en el programa. Entender y preguntar antes de actuar.

## Flujo real del proceso (levantado el 11-06-2026 — reglas firmes)

- **El trabajo es una cadena de ciclos**: MP programada → ejecución o causal
  → papel → firma → carpeta física → recién al final el Excel oficial. El
  desorden del usuario = ciclos abiertos invisibles. Toda vista nueva debe
  mostrar el ciclo y su siguiente paso, no solo datos por pestaña.
- **Orden de registro**: 1º GEB con el detalle completo (fecha, ejecutor, qué
  se hizo — la trazabilidad que antes no existía). 2º papel firmado y
  archivado en la carpeta del equipo. 3º RECIÉN AHÍ el código de resultado al
  Excel oficial. Celda vacía en el Excel = ciclo abierto. La lista "falta
  traspasar al Excel" debería ofrecer solo lo que ya tiene papel archivado.
- **Rojo = papel pendiente**: causal registrada cuyo documento no está
  "archivado" en `S.docflow`. El semáforo debe verse donde se revisa.
- **Reprogramación implícita (detectable)**: resultado vacío + ejecución en un
  mes posterior ⇒ hubo reprogramación de facto → falta registrar la causal e
  imprimir su Anexo 3. GEB debe marcarlo solo.
- **Revisión caso a caso, papeleo en lote**: la causal la decide SIEMPRE el
  usuario, caso a caso, con la evidencia al lado (correctivo abierto, estado,
  préstamo, familia externa, fichas, ejecución posterior). Solo el papeleo se
  agrupa: llenar todos los vacíos → filtrar rojos → por servicio → imprimir
  en lote → repartir. La impresión es la última etapa, nunca de a uno.
- **Portador del papel**: cada documento impreso lleva un portador asignable
  (por defecto quien tenía asignada/ejecutó esa MP; a veces el usuario).
  "Hoy" debe recordar qué firmas verificar y a quién.
- **Los 3 papeles** (procedimiento oficial PR-DC-0113/EQ2.1 v10, PDF en la
  carpeta del proyecto): protocolo MP (Anexo 2 por familia; firma técnico
  ejecutor + jefe SEC + VºB servicio), reporte de reprogramación (Anexo 3;
  jefe SEC + supervisora; el formato oficial admite VARIOS equipos del mismo
  servicio, cada fila con su causal), retiro de circulación (Anexo 4; jefe
  SEC + supervisora). `formReprog` hoy imprime una hoja por equipo.
  **Pregunta abierta antes de tocar impresión**: ¿el archivo en carpetas
  individuales exige hoja por equipo o sirven copias del Anexo 3 grupal?
- **Próxima fase propuesta (espera OK)**: vista **"Revisión y cierre"** en
  Plan MP — todos los vacíos de meses pasados en una lista única, evidencia
  automática, causal asignable en línea, semáforo rojo de papel; conectada a
  Documentos (lote y estados) y al traspaso a Excel condicionado a papel
  archivado. Después: Anexo 3 agrupado por servicio + portador.

## Método de trabajo (cómo avanzamos sin retroceder)

- **Fases.** Todo trabajo nuevo se divide en fases pequeñas registradas en
  `PLAN.md` (por decidir / pendiente / en curso / hecha). Una fase a la vez:
  la siguiente no se abre sin que el usuario valide la anterior.
- **Anti-regresión.** Lo que ya funciona es intocable salvo acuerdo explícito.
  Antes de dar una fase por terminada: probar con los respaldos JSON reales y
  verificar que las pestañas y flujos existentes siguen funcionando. Si algo
  se rompe, revertirlo es la prioridad número uno. Commits pequeños con
  mensaje claro.
- **Entender antes de ejecutar.** Si el "para qué" de una petición no es
  evidente y no está en este archivo, hacer 2 a 4 preguntas concretas, nunca
  más. Si existe una forma mejor de lograr el fin real, proponerla en 2-3
  líneas junto a lo pedido; el usuario decide.
- **Comunicación.** Respuestas cortas y al grano; nada de muros de texto ni
  listas de todo lo posible. Cero explicaciones técnicas salvo que el usuario
  las pida o las necesite para decidir (máximo 3 líneas, lenguaje simple). Al
  terminar algo, indicar cómo probarlo en 1-2 pasos.
- **Aprendizaje.** Cada decisión nueva, preferencia o "para qué" descubierto
  se anota en este mismo archivo al cerrar la fase, y el avance se refleja en
  `PLAN.md`. Estos dos archivos son la memoria del proyecto entre sesiones:
  mantenerlos al día es parte del trabajo, no un extra.

## Arquitectura (decisiones firmes)

- **Un solo archivo `index.html`**: sin servidor, sin internet, sin librerías
  externas. Abre con doble clic en Chrome/Edge. Los datos viven en
  `localStorage` (clave `geb_hrt_v3`); respaldo/restauración JSON en Datos.
- **La app parte VACÍA**: todo entra importando el `.xlsm` oficial
  (lector ZIP propio con `DecompressionStream` + parsing XML por regex).
  La importación es una **fusión sin pérdida**: el archivo manda en
  maestro/plan/resultados (columnas Q-Observación y S-Responsable excluidas);
  lo registrado en la app se conserva; reporta diferencias en ambos sentidos
  ("falta traspasar al Excel" es la lista clave, porque el Excel es el
  documento oficial).
- **Generador de .xlsx propio** (`zipCrear`/`xlsxCrear` con CRC32 y
  styles.xml): exportaciones con formato profesional (título azul, fecha,
  encabezado blanco/azul) y lista desplegable por validación de datos
  (asignaciones). PDF = imprimir → guardar como PDF.
- **Sistema de filtros tipo Excel genérico** (`fcCfg`/`fcFilas`/`thFC`/
  `dropFC` + estado `FCF` por tabla): lo usan Inventario, Plan MP,
  Asignación, Distribuciones, Informes y Documentos. Cualquier tabla nueva
  debe usarlo.
- **Estado del equipo NUNCA se edita a mano**: deriva de eventos (falla→No
  operativo, envío→En ST, entrega→Operativo, formulario de ejecución de MP,
  eventos de ficha con estado). Se eliminó el selector manual a propósito.
- **Generador de reportes técnicos** (protocolos imprimibles por familia) va
  embebido como string `REP_SRC` en un **iframe** (aislamiento de CSS) y se
  alimenta del inventario en vivo (`datosReportes()`). Tamaño carta al 100%.
- **Todo recuadro/fila con detalle es clickeable completo** (`clickFila`
  ignora controles internos); los números de tablas resumen navegan a la
  vista filtrada correspondiente.
- Render: `render()` redibuja `#main` por pestaña y **restaura el foco** del
  input activo (crítico para búsqueda en vivo; no romper).

## Mapa de pestañas (el "para qué" de cada una)

- **🌅 Hoy** (inicio): el día ordenado — sapo, urgentes, plazos, perseguir ST,
  avance del mes, sincronización con Excel, acciones rápidas.
- **📊 Panel**: números para jefatura + todas las alertas (motor en
  `calcAlertas`: plazos 30 días, C2/C3/C4 en seguimiento, correctivos
  estancados, informes de empresa pendientes, pendientes vencidos).
- **🗂 Inventario**: Listado (11 columnas, tarjetas de estado clickeables,
  días en estado, export .xlsx nombrado según filtro) y Distribución por
  Servicio/Equipo (números navegables).
- **🗓 Plan MP**: Control de ejecución (registrar Si abre formulario con
  fecha/ejecutor/estado del equipo/observaciones → `S.mpEjec`; causales con
  plazo) + Distribución (por técnico con % y números navegables; servicio ×
  familia) + botón **✅ Cierre de mes** (checklist + resumen jefatura).
- **👷 Asignación**: asignar ejecutores del mes, exportar .xlsx con
  desplegable, **subir asignaciones** de vuelta (mapea por ID), y
  Distribución del último evento preventivo (descarga por responsable).
- **📁 Documentos**: derivados AUTOMÁTICAMENTE de la planilla (causal →
  reporte de reprogramación; Si → protocolo; externas → + informe empresa).
  Estados: imprimir → entregado → archivado (`S.docflow`; los de MP enlazan
  con `S.docs`). **Impresión en lote** del formulario de reprogramación con
  firmas (`formReprog`). Mes cerrado = cero documentos pendientes.
- **📄 Informes**: informe mensual por servicio clínico, filtrable, para
  imprimir/exportar y enviar.
- **🛠 Correctivos**: casos con hitos cronológicos, días en estado, bitácora
  de seguimiento fechada; cerrar por entrega dispara aviso de MP pendiente
  al retorno (C2/C3/C4).
- **🧾 Reportes**: protocolos técnicos imprimibles (iframe, carta 100%).
- **📌 Pendientes**: SOLO tareas reales (no documentos). Lista por defecto;
  tablero opcional; delegación con nombre (`p.deleg`) y verificación en Hoy.
- **⚙️ Datos**: importar maestro, respaldos JSON, exportaciones, ejecutores.

## Modelo de datos (localStorage `geb_hrt_v3`)

`S = { version:3, equipos:[{id, carpeta, inv, fam, equipo, servicio, unidad,
ubicacion, proc, marca, modelo, serie, anio, clasif, obs, frec, respMP,
plan[12], resultado[12][2], obsReg, estado, baja}], fichas:{eqId:[{f,t,e,st}]},
correctivos:[{id,eqId,fecha,folio,ingeniero,descripcion,hitos,seguimiento,
cerrado}], pendientes:[{id,titulo,eqId,limite,prio,sapo,deleg,sub,updates,
done,creado}], asig:{mes:{eqId:resp}}, docs:{"id-m":{int,emp}},
reprog:{"id-m":{causal,destino}}, mpEjec:{"id-m":{f,e,st,o}},
docflow:{key:{st,f}}, responsables:[11 ejecutores], config, ultimaImport }`

## Cómo probar (sin navegador)

Extraer el script principal de index.html y evaluarlo en Node con stubs de
DOM/localStorage (ver patrón en commits): elementos por id con getEl(),
`render()` por pestaña, y flujos con los **respaldos JSON reales del
usuario**. El lector/generador xlsx se valida con openpyxl en Python.

## Estado actual e ideas pendientes (no comprometidas)

- El usuario evaluará qué pestañas usa de verdad para PODAR el programa
  (minimalismo). Preguntar el para qué de cada una antes de eliminar.
- Ideas mencionadas no implementadas: gráfico de evolución mensual de
  cumplimiento; % operativo por familia (disponibilidad); imprimir protocolos
  del mes por técnico desde el Plan; recordatorio de respaldo semanal;
  acciones en lote (varios equipos a la vez); unificar nombre del hospital
  (GEB dice "Hospital Regional de Temuco", los reportes técnicos "Hospital
  Doctor Hernán Henríquez Aravena") — preguntar cuál.
