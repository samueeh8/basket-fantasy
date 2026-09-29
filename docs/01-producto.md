# Producto y decisiones pendientes

## Encargo confirmado

Construir progresivamente un fantasy de Liga Endesa, con perspectiva comercial futura, arquitectura completa y presupuesto inicial de servicios de 0 €. La planificación debe permitir ensamblar y comprobar el sistema tras cada paso. El usuario ha confirmado liga privada, desarrollo local y temporada objetivo 2026/27.

La investigación previa es una hipótesis de partida, no una auditoría de datos ni una licencia. No se consideran confirmados ni el acceso Free a la temporada objetivo ni la completitud de estadísticas por jugador.

## Alcance inicial confirmado y propuestas restantes

Primera versión: liga privada. Desarrollo y pruebas en local; una URL se preparará cuando se necesite. Temporada objetivo: ACB 2026/27, con intención de probar datos reales durante el desarrollo. La web adaptable al móvil, el acceso por invitación y el piloto de 8–10 amigos siguen como diseño recomendado; falta concretar participantes y límites. Ciclo completo: entrar, crear/unirse a liga, conseguir jugadores, gestionar equipo, alinear, recibir puntos, ver clasificación y repetir jornada.

Se propone inicialmente dinero ficticio, sin cuotas de entrada, apuestas ni premios económicos. Debe confirmarse en D16; introducir dinero real cambia el alcance de producto, operación y revisión legal.

Quedarían después del primer ciclo: portal público editorial, predicciones, noticias, lesiones automatizadas, chat, notificaciones push, aplicaciones nativas, cláusulas, múltiples competiciones, escudos/fotos oficiales y datos en directo. Las transferencias entre usuarios sí forman parte del objetivo; su mecanismo está por decidir.

## Decisiones de producto

Las respuestas confirmadas se indican expresamente. El resto se resolverá antes de programar el módulo correspondiente. El desarrollo local no necesita esperar a que todas las reglas estén cerradas.

| ID | Pregunta concreta | Propuesta u opciones | Necesaria antes de |
| --- | --- | --- | --- |
| D01 | ¿Solo fantasy privado al principio o también portal público? | CONFIRMADO: liga privada; portal público fuera de primera versión | Cierre P00 |
| D02 | ¿Local primero o URL desde la primera entrega? ¿Equipo disponible y experiencia técnica? | CONFIRMADO: local primero; URL cuando se necesite. Inventario técnico pendiente | P02 |
| D03 | ¿Qué temporada y fases se juegan? ¿Tienes cuenta API y acceso Free? | CONFIRMADO: 2026/27; proveedor por elegir. Fases y acceso autenticado pendientes | P01 |
| D04 | ¿Cómo se inicia sesión? | OAuth Google propuesto para beta gratuita; email depende de SMTP verificable | P04 |
| D05 | ¿Cuántos miembros y ligas por usuario? ¿Qué puede hacer el administrador de liga? | Invitación revocable; límites y facultades pendientes | P04 |
| D06 | ¿Un jugador solo puede pertenecer a un manager por liga? | CONFIRMADO: exclusivo por liga. Un jugador puede pertenecer a otro manager en otra liga | P05 |
| D07 | ¿Plantilla inicial vacía, reparto aleatorio, draft u otra? | CONFIRMADO: opción con/sin plantilla al crear liga. Pendiente método de asignación, tamaño y compensación | P05 |
| D08 | ¿Presupuesto, tamaño de plantilla, posiciones y saldo negativo permitido? | CONFIRMADO: calibrar presupuesto junto a mercado y valores; sin importe arbitrario. Resto pendiente | P05 |
| D09 | ¿Cómo salen jugadores libres y cómo se compran? | CONFIRMADO: el sistema ofrece varios jugadores por día; pujas secretas. Cada día se adjudican al cierre al mayor importe. Solo se muestra el número de pujas activas, nunca identidad ni importe ajenos | Diseño económico previo a P05; implementación P06 |
| D10 | ¿Qué ocurre al empatar pujas, cancelar, no tener saldo o adjudicar varios jugadores? | Orden determinista, reservas y prioridad pendientes de reglas | P06 |
| D11 | ¿Cómo son ventas y traspasos entre usuarios? | Oferta directa/listado; comisiones, precios mínimos, controles de abuso pendientes | P06 |
| D12 | ¿Cuántos titulares/suplentes, posiciones y cambios? | Capitán, bonus, sustituciones y límites por club pendientes | P07 |
| D13 | ¿Cuándo se bloquea una alineación y cómo se tratan aplazamientos? | Jornada completa o por jugador/partido; no decidir por conveniencia técnica | P07 |
| D14 | ¿Qué fórmula de puntos se quiere? | Tres candidatas del usuario: nota sobre 10, valoración, fórmula propia con acciones/resultado/sanciones. Ninguna seleccionada; auditar campos antes | P08; antes si determina precios iniciales |
| D15 | ¿Clasificación acumulada o enfrentamientos? ¿Desempates, correcciones y premios ficticios? | Acumulada recomendada por sencillez; pendiente de confirmación | P08 |
| D16 | ¿Habrá dinero real, cuotas, premios, publicidad o menores? ¿Países objetivo? | Beta privada sin dinero real y público adulto propuesta | P11; antes si respuesta amplía alcance |
| D17 | ¿Cuánto retraso de resultados es aceptable? ¿Se acepta una demo sintética si Free no cubre ACB actual? | Resultados tras partido/jornada propuestos; no prometer live | P09/P11 |
| D18 | ¿Nombre, identidad visual, participantes y responsable de soporte/datos personales? | Nombre del repositorio provisional; recursos gráficos propios | P11 |
| D19 | ¿El valor del jugador es fijo o dinámico y por liga o global? | CONFIRMADO: diseñarlo junto al presupuesto. Separar precio base, operación y valor calculado; fórmula y actualización pendientes | Diseño económico previo a P05; evolución P12 si se aplaza |

Registrar respuesta, fecha y motivo debajo de esta tabla cuando se reciban. Si cambia una regla con ligas activas, crear una versión y definir desde cuándo se aplica; no reescribir silenciosamente la historia.

## Respuestas recibidas · 2026-09-29

- Liga privada, pruebas en local y temporada 2026/27 confirmadas.
- La creación de liga debe ofrecer empezar con plantilla o sin ella. No se ha confirmado reparto aleatorio ni draft.
- El presupuesto se determinará en función del mercado y de los valores, no al azar.
- Se contemplan tres sistemas de puntuación. El usuario propone considerar aciertos, fallos, faltas, victoria/derrota, técnicas, antideportivas y expulsiones en una posible fórmula propia; faltan pesos y disponibilidad de datos.
- El usuario admite estudiar scraping de Flashscore/Sofascore u otra alternativa si no existe API gratuita suficiente. Esto autoriza evaluar la vía, no acredita cobertura ni permiso de los sitios. Ver la auditoría actualizada.
- Se confirma exclusividad por liga: un único manager puede poseer activamente a un jugador en esa liga; el mismo jugador puede existir en plantillas de otras ligas.
- Mercado confirmado: pujas secretas. La ficha/listado de mercado muestra la cifra total de pujas de cada jugador, incluida la propia si existe; cada manager puede ver y modificar solo su propia puja. No se muestran identidades ni cantidades de terceros.
- Confirmado el ciclo del mercado: el sistema ofrece varios jugadores cada día y, al cierre diario, cada jugador se adjudica a quien haya pujado más.

Desarrollo de estas decisiones: [reglas y calibración económica](08-reglas-economia.md).

## Pantallas del primer ciclo

| Pantalla | Información y acciones | Estados que deben diseñarse |
| --- | --- | --- |
| Acceso | Entrar/salir, sesión caducada, invitación | Error OAuth, invitación inválida, cuenta sin liga |
| Mis ligas | Crear, unirse y elegir liga | Sin ligas, límite alcanzado, acceso revocado |
| Resumen de liga | Jornada, posición, saldo, actividad | Liga no iniciada, datos desactualizados |
| Catálogo/ficha | Buscar, filtrar, ver equipo, posición y estadísticas disponibles | Campo desconocido, jugador sin estadísticas, sin coincidencias |
| Mi equipo | Plantilla, saldo disponible y comprometido | Plantilla incompleta, jugador transferido/baja, acción inválida |
| Mercado | Lote diario de jugadores; pujas secretas; número de pujas activas y mi propia puja; cierre con ganador por importe; después, traspasos según D11 | Operación en curso, plazo vencido, saldo insuficiente, conflicto simultáneo |
| Alineación | Selección y hora límite | Incompleta, bloqueada, cambios de calendario |
| Jornada | Calendario y puntos desglosados | No empezada, provisional, aplazada, rectificada |
| Clasificación | Puntos por jornada y total | Empate, recalculando, versión de resultados |
| Ajustes | Perfil, salir de liga/cuenta según reglas, privacidad | Acción con impacto en liga, solicitud en curso |
| Administración | Estado de ingesta, anomalías, reprocesado y trazabilidad | Sin permisos, proveedor caído, cuota agotada |

La administración técnica es un rol distinto del administrador de liga. Los permisos se especifican antes de mostrar cada acción.

## Criterio de éxito de la beta

Propuesta a confirmar: un grupo completa al menos dos jornadas con compras/traspasos, alineaciones y clasificación entendible; ningún saldo ni propietario queda inconsistente; se puede corregir un dato y explicar el resultado. Se registran errores, tareas que los participantes no entienden y motivos para volver.

Medir de forma mínima: participantes activos por jornada, equipos alineados a tiempo, operaciones completadas/fallidas y retorno a la siguiente jornada. No fijar como objetivos reales las cifras hipotéticas de usuarios o retención del texto inicial.
