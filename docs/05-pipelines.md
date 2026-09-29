# Mapa de entregas incrementales

Cada Pxx es un bloque funcional; cada Pxx.n es una tarea pequeña. Completar y demostrar una tarea antes de abrir la siguiente dependiente. No son semanas ni estimaciones de calendario: el ritmo depende de reglas, acceso a datos y disponibilidad del desarrollador.

## Contrato de cada tarea

Antes: objetivo, dependencias, decisiones, límite de alcance y ejemplo de aceptación. Durante: migración/permisos → caso de uso/API → interfaz → comprobación integrada. Después: demo, pruebas necesarias, documentación y siguiente paso. Para cambios sin interfaz (por ejemplo una restricción), usar una comprobación reproducible equivalente.

Un paso no termina con «está el frontend» o «hay una tabla»: termina cuando su comportamiento se puede comprobar. Las pantallas sintéticas estarán etiquetadas; no se presentarán como datos ACB reales.

## P00 · Alcance y forma de trabajar

**Resultado:** saber qué versión estamos construyendo y qué decisiones siguen abiertas.

- [x] P00.1 Registrar alcance inicial: liga privada, local primero y temporada 2026/27. Acceso al proveedor y fases de competición se concretan en P01.
- [ ] P00.2 Confirmar la selección técnica o registrar preferencias concretas del usuario.
- [ ] P00.3 Elegir una tarea lista y abrir su ficha con la plantilla; fijar responsable de decisiones.

**Aceptación:** alcance de primera versión escrito; regla desconocida identificada, no inventada; estado y siguiente tarea coinciden. P00.1 está resuelto; falta concretar la siguiente ficha de trabajo y revisar preferencias técnicas si las hay.

## P01 · Viabilidad de datos y uso

**Depende:** D03. Puede avanzar junto a P02/P03, sin necesidad de desarrollar en paralelo con varios agentes.

- [ ] P01.1 Registrar cuenta/producto/plan, temporada y acceso a clave local; comprobar cuota y catálogo.
- [ ] P01.2 Auditar equipos, IDs y plantillas con paginación y nulos.
- [ ] P01.3 Auditar calendario y una muestra de estadísticas por jugador.
- [ ] P01.4 Medir actualización/correcciones en consultas separadas y simular fallos.
- [ ] P01.5 Completar matriz de disponibilidad, calidad, frecuencia, derechos y alternativas; preparar preguntas al proveedor si hacen falta.
- [ ] P01.6 Emitir resultado técnico y de uso independientes, con presupuesto de llamadas.

Avance documental: TheSportsDB responde a consultas Free de metadatos ACB y calendario 2026/27 (cinco eventos recibidos; completitud no probada). API-Basketball sigue pendiente de clave. Clasificación técnica del proveedor principal: SIN EVIDENCIA autenticada todavía; ver `04-auditoria-proveedor.md`.

**Demo:** informe reproducible de una muestra ACB, sin exponer claves. **Aceptación:** conclusiones sustentadas en respuestas reales, limitaciones visibles y puerta de publicación definida. Si no hay permisos, el resultado de uso sigue pendiente aunque lo técnico sea apto.

## P02 · Base local reproducible

**Depende:** decisión de entorno D02. No depende de datos reales.

- [ ] P02.1 Inventariar Node/npm/Git/contenedores; comprobar recursos y puertos. Documentar instalación mínima sin modificar el equipo indiscriminadamente.
- [ ] P02.2 Crear React/Vite/TypeScript y un Worker Hono con `/api/health`; interfaz muestra conexión correcta/error.
- [ ] P02.3 Añadir Supabase local y primera migración sintética; demostrar una lectura desde UI a través del backend.
- [ ] P02.4 Probar una función transaccional mínima y denegación de escritura no autorizada; comprobar que el acceso HTTPS sirve desde el runtime elegido.
- [ ] P02.5 Añadir `.gitignore`, `.env.example`, scripts de calidad, archivo de bloqueo y README de arranque realmente probado.
- [ ] P02.6 Configurar CI si hay repositorio remoto; mientras tanto dejar comprobaciones locales equivalentes. Probar compilación de producción.

**Demo:** desde instalación documentada se arranca, se crea la BD y se ve un registro sintético. **Aceptación:** secretos excluidos, frontend/backend/BD conectados, error de BD entendible, build y tipos correctos. Sin cuentas cloud obligatorias.

## P03 · Catálogo útil y diseño mínimo

**Depende:** P02.

- [ ] P03.1 Crear equipos/jugadores/IDs internos con datos sintéticos, migraciones e índices mínimos; API paginada.
- [ ] P03.2 Mostrar listado responsive, búsqueda y filtros con estados de carga/error/vacío.
- [ ] P03.3 Añadir ficha, abreviaturas y avatar propio; mostrar campos desconocidos como desconocidos.
- [ ] P03.4 Definir colores, tipografía del sistema, espaciado, botones/formularios/tablas reutilizables y navegación de teclado.
- [ ] P03.5 Separar adaptador sintético del contrato de proveedor; probar que cambiar adaptador no modifica la pantalla ni los IDs propios.

**Demo:** buscar un jugador, abrir ficha, navegar en móvil y recuperar un error. **Aceptación:** no hay fotos/escudos remotos ni consultas al proveedor desde el navegador; tests de filtros y contrato; tamaño de página limitado.

## P04 · Acceso, ligas y aislamiento

**Depende:** P03 y D04–D05.

- [ ] P04.1 Configurar Auth local, perfil mínimo, login/logout y sesión caducada; decidir persistencia de sesión.
- [ ] P04.2 Crear una liga con versión de reglas todavía en borrador y listar solo las ligas del usuario.
- [ ] P04.3 Crear/aceptar/revocar invitación con token impredecible, caducidad y límites; aceptación atómica.
- [ ] P04.4 Mostrar miembros y separar roles de miembro, administrador de liga y operador de plataforma.
- [ ] P04.5 Probar dos ligas y varias identidades, manipulando IDs y llamando a RPC directamente.

**Demo:** A invita a B; C ajeno no puede leer ni modificar la liga. **Aceptación:** RLS y autorización del servidor probadas, invitación inválida no filtra datos, cerrar sesión limpia información privada. Las reglas sin aprobar mantienen la liga sin iniciar.

## P05 · Equipo inicial y economía verificable

**Depende:** P04 y D06–D08; el diseño económico requiere acordar la base del mercado D09 y valores D19 antes de fijar saldo. Esto es especificación previa, no depende de implementar P06.

- [ ] P05.0 Calibrar precios, capacidad de plantillas y saldo según `08-reglas-economia.md`; comparar modalidades con/sin plantilla. Resolver pesos de puntuación antes si el modelo de precios los utiliza.
- [ ] P05.1 Crear equipo fantasy y monedero; inicialización idempotente con asiento de saldo inicial.
- [ ] P05.2 Implementar selector con/sin plantilla al crear liga y el método de asignación aprobado; validar capacidad, compensación y exclusividad por liga.
- [ ] P05.3 Mostrar plantilla, saldo contable/disponible y libro de movimientos; diferenciar dinero ficticio.
- [ ] P05.4 Validar invariantes con alta duplicada, peticiones simultáneas y fallo de transacción.

**Demo:** iniciar una liga y comprobar que repetir la inicialización no entrega más dinero ni jugadores. **Aceptación:** suma contable reconciliada, propiedad válida, restricciones de BD y denegación de modificación directa.

## P06 · Mercado y traspasos

**Depende:** P05 y D09–D11; D19 cuando afecte a precios/ventas. Si se elige otro mercado, reescribir las subtareas específicas antes de programarlas.

- [ ] P06.1 Especificar lote de varios jugadores diario, pujas secretas, mayor importe al cierre, estados y ejemplos; precisar hora/zona, empates, saldo y prioridad. Fijar que el contador es el total de pujas activas, incluida la propia, sin identidad ni importe ajenos.
- [ ] P06.2 Mostrar ventana/listado de mercado, contador de pujas y mi propia puja; crear una puja.
- [ ] P06.3 Implementar actualización/cancelación y reserva de saldo si se elige; garantizar que el contador se mantiene correcto y que los rivales no reciben detalle de pujas.
- [ ] P06.4 Adjudicar una operación atómicamente: saldo, propiedad, asiento, estado e idempotencia.
- [ ] P06.5 Añadir adjudicación diaria reanudable de todos los jugadores del lote, con orden/prioridad aprobados y atomicidad por jugador; resultado y explicación en UI.
- [ ] P06.6 Incorporar traspaso entre usuarios mediante el mecanismo elegido y venta al sistema solo si se aprueba.
- [ ] P06.7 Probar empate, saldo insuficiente, dos compradores, dos gastos simultáneos, plazo vencido, respuesta perdida y reejecución del job; comprobar que solo se expone el contador total y que actualización/cancelación lo ajustan correctamente.

**Demo:** dos managers compiten/compran según reglas y después realizan un traspaso; saldos y propietario coinciden con el historial. **Aceptación:** ninguna duplicación, filtración de pujas privadas ni operación parcial. El reloj del navegador no permite comprar fuera de plazo.

## P07 · Jornada y alineación

**Depende:** P06 y D12–D13; calendario sintético.

- [ ] P07.1 Modelar jornadas y sus partidos, estados, fechas y política aprobada de aplazamientos.
- [ ] P07.2 Mostrar calendario y permitir guardar alineación con validación de propietario, tamaño y posiciones.
- [ ] P07.3 Implementar bloqueo temporal y snapshots; controlar edición concurrente por versión.
- [ ] P07.4 Aplicar casos de aplazamiento, jugador transferido, cambio de posición y horario de verano/invierno.

**Demo:** guardar antes del cierre, rechazar después y conservar el equipo histórico tras un traspaso. **Aceptación:** una ejecución tardía del cron no amplía el plazo; usuario no puede alinear jugadores ajenos ni de otra liga.

## P08 · Puntos y clasificación

**Depende:** P07 y D14–D15; campos de fórmula validados por P01 para uso real. Si la auditoría sigue pendiente, solo prueba sintética con regla explícitamente aprobada.

- [ ] P08.1 Comparar nota sobre 10, valoración y fórmula propia con los datos disponibles; seleccionar una primera fórmula, versionado/redondeos y ejemplos de cálculo manual. No construir tres modos sin decisión explícita.
- [ ] P08.2 Importar un partido sintético final e incompleto; calcular puntos solo cuando proceda.
- [ ] P08.3 Puntuar snapshots de una jornada y mostrar desglose por jugador y término.
- [ ] P08.4 Publicar clasificación con desempates aprobados y revisión identificable.
- [ ] P08.5 Corregir un dato, recalcular sin duplicar y mantener la revisión anterior trazable.
- [ ] P08.6 Completar un ciclo de juego sintético: liga → mercado → alineación → partido → clasificación → siguiente jornada.

**Demo:** cálculo manual y aplicación coinciden; una corrección cambia exactamente lo esperado. **Aceptación:** ningún ausente convertido en cero, recalculado determinista y sin mezclar revisiones. Aquí existe el primer juego completo con datos de prueba.

## P09 · Conectar ACB real

**Depende:** P08 y P01 apto para alcance/frecuencia previstos; publicación requiere uso aclarado.

- [ ] P09.1 Implementar cliente autenticado y normalizador con contratos reales auditados.
- [ ] P09.2 Incorporar IDs externos, upserts y resolución de ambigüedades; probar reimportación sin pérdida de relaciones fantasy.
- [ ] P09.3 Añadir cuotas, prioridades, reintentos y cursores; separar importación inicial de sincronización normal.
- [ ] P09.4 Importar calendario/plantillas/estadísticas y reconciliar anomalías antes de puntuar.
- [ ] P09.5 Mostrar origen, última actualización, estado provisional y proveedor caído; no ocultar retrasos.
- [ ] P09.6 Ejecutar una jornada en modo ensayo y comparar con la muestra auditada; comprobar coste diario real.

**Demo:** una jornada real recorre el mismo camino ya probado con datos sintéticos. **Aceptación:** reglas compatibles con los campos, cuota dentro del tope, cero exposición de clave y estado de derechos documentado. No mezclar datos sintéticos y reales en una liga activa.

## P10 · Alojamiento gratuito y operación

**Depende:** P08 para ensayo completo. El ensayo mínimo puede adelantarse tras P03 si D02 pide URL temprana; usar datos sintéticos y acceso restringido.

- [ ] P10.1 Revisar de nuevo planes, condiciones y cuotas; configurar cuentas gratuitas del usuario sin servicios facturables ni dominio comprado.
- [ ] P10.2 Crear entorno de beta con datos separados, migraciones reproducibles y secretos por entorno.
- [ ] P10.3 Publicar build en subdominio gratuito, configurar Auth/redirects exactos y HTTPS.
- [ ] P10.4 Medir CPU real del Worker y cron, número de subrequests, egress y tamaño BD con ciclo completo.
- [ ] P10.5 Configurar trabajos recuperables, panel de fallos, logs sanitizados y comprobaciones de cuota.
- [ ] P10.6 Hacer copia y restauración en entorno aislado; ensayar rollback de aplicación compatible con esquema.
- [ ] P10.7 Ejecutar pruebas de acceso cruzado, abuso, rutas privadas, caché y flujo móvil en URL real.

**Demo:** acceder desde otro dispositivo, operar, recuperar un trabajo interrumpido y restaurar copia. **Aceptación:** presupuesto 0, límites medidos con margen, permisos intactos, costes de exceso desactivados o sin activación facturable. Si el runtime no cabe, volver a decisión técnica, no activar pago.

## P11 · Beta privada con amigos

**Depende:** P09 + P10, D16–D18 y lista de salida de seguridad completada. Una demo sintética con amigos es otro alcance y se identificará como tal.

- [ ] P11.1 Congelar reglas de la liga piloto, guía de uso, aviso de privacidad y expectativas de actualización.
- [ ] P11.2 Incorporar participantes, verificar invitaciones/acceso y recoger dudas sin recopilar datos innecesarios.
- [ ] P11.3 Completar primera jornada vigilando cuotas, ingesta, adjudicaciones y puntos.
- [ ] P11.4 Corregir incidencias y completar una segunda jornada; registrar retorno y operaciones.
- [ ] P11.5 Evaluar diversión, comprensión, estabilidad y coste; elegir la siguiente mejora con evidencia.

**Aceptación:** ciclo completo repetible, ningún fallo crítico abierto de dinero/propiedad/permisos, restauración comprobada y participantes capaces de explicar sus puntos. No extrapolar capacidad a 1.000 usuarios sin medir.

## P12 · Evolución por prioridad

No construir todo al acabar beta. Elegir un bloque con necesidad demostrada, presupuesto y criterio de éxito propios.

| Bloque | Dependencias | Primera entrega pequeña |
| --- | --- | --- |
| Valores dinámicos | D19, histórico suficiente y controles de abuso | Precio diario versionado, explicado y reproducible |
| Tendencias/propiedad | Definición de universo y denominadores | Una métrica agregada sin revelar pujas ni ligas privadas |
| Comparador | Estadística fiable y diseño aprobado | Comparar dos jugadores con mismo periodo y datos ausentes visibles |
| Disponibilidad | Fuentes permitidas y responsable editorial | Estado con fuente, fecha y caducidad; no diagnosticar lesiones |
| Noticias | Política editorial y derechos | Enlaces y resúmenes propios permitidos; sin copiar artículos |
| Predicciones | Histórico, baseline y evaluación temporal | Media/base simple con incertidumbre; sin APIs de IA pagadas |
| Live | Cobertura, derechos y presupuesto de llamadas | Un ensayo limitado que mida latencia/coste antes de ofrecerlo |
| PWA/notificaciones | Demanda y flujo web estable | Instalación y aviso dentro de app antes de push/email |
| Portal público/SEO | D01 y necesidad de captación | Una página indexable; revisar renderizado sin rehacer el juego |
| Licencias/proveedor premium | Métricas, autorización de contacto y presupuesto | Dossier de producto y comparativa, sin contratar automáticamente |
| Escala/comercialización | Carga medida, privacidad, soporte y presupuesto | Prueba de capacidad y modelo de operación antes de abrir registro |

## Pipeline de integración continua

`cambio pequeño → formato/lint/tipos → pruebas relevantes → migraciones y RLS si cambian → build → revisión → despliegue controlado → smoke test → actualizar estado`.

Tests de lógica no llaman al proveedor real. Pruebas de integración usan PostgreSQL/Auth locales y fixtures sintéticos. E2E cubre el ciclo crítico, con ampliación al cambiar comportamiento. Migraciones remotas no se ejecutan desde PRs no confiables ni con secretos expuestos. Detalle de recuperación en `06-seguridad-operacion.md`.
