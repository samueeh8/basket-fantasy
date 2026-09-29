# Seguridad, calidad y operación

Estas medidas se incorporan en el módulo correspondiente. P10/P11 comprueban el conjunto; no se pospone toda la seguridad al final.

## Modelo de amenazas y permisos

Activos: cuentas, ligas privadas, pujas/ofertas, saldos ficticios, propiedad de jugadores, puntuaciones, credenciales y continuidad de la competición. Escenarios principales: usuario de otra liga, miembro manipulando peticiones, doble clic/reintento, operaciones concurrentes, clave expuesta, proveedor incompleto y tarea interrumpida.

| Actor | Puede | No puede |
| --- | --- | --- |
| Visitante | Acceder a login y contenido explícitamente público | Enumerar ligas/invitaciones o leer datos privados |
| Usuario | Consultar su perfil y ligas, aceptar invitación válida | Asignarse roles o introducir saldo |
| Miembro de liga | Ejecutar acciones de juego autorizadas y ver el contador de pujas activas por jugador | Cambiar otra liga, ver identidad o importe de pujas ajenas, editar puntos |
| Administrador de liga | Gestionar solo las acciones aprobadas en D05 | Acceder a claves, alterar historial o saltarse reglas de mercado |
| Operador de plataforma | Ingesta, revisión, reintentos y soporte trazable | Usar una identidad compartida o dejar cambios sin motivo |
| Trabajo de sistema | Operación concreta para la que fue habilitado | Aceptar instrucciones libres o URLs arbitrarias desde usuarios |

## Controles por área

| Riesgo | Control | Entrega y prueba |
| --- | --- | --- |
| Acceso a otra liga | Autorización de objeto + RLS + FK/coherencia de liga | P04: alterar IDs y llamar API/RPC directamente |
| JWT falso/caducado | Verificación criptográfica y claims; no decodificar y confiar | P04: token modificado, caducado y de otro proyecto |
| Rol falsificado | Roles de fuente controlada por servidor; no metadatos editables | P04: intento de autoasignación |
| Filtración de pujas | Políticas de lectura específicas: rival recibe solo contador agregado; postor recibe además únicamente su propia puja | P06: consultar como rival/visitante y revisar respuesta/API directa y caché antes/después del cierre |
| Doble compra/gasto | Locks, restricciones, transacción e idempotencia | P05/P06: peticiones concurrentes y reintento tras timeout |
| Fraude de hora/puntos | Tiempo BD, snapshots y cálculo del servidor | P07/P08: cambiar reloj/payload del navegador |
| XSS | Escapado, texto sin HTML arbitrario, CSP y dependencias revisadas | Desde P03: nombres con caracteres/markup malicioso |
| CSRF/cookies | Si se usan cookies: SameSite, Secure, HttpOnly y control de origen/token | P04: mutación desde origen no permitido |
| CORS | Mismo origen en producción; lista exacta si se necesita excepción | P10: origen ajeno rechazado |
| Inyección SQL | Parámetros tipados; sin SQL concatenado con entradas | P02 en adelante: entradas no válidas y revisión |
| Abuso de endpoints | Límite de cuerpo/página, cuotas por identidad e IP y validación temprana | P04/P10: ráfagas, invitaciones, búsquedas y 429 |
| Secretos | Variables privadas por entorno, sin prefijo público Vite; rotación | P02/P10: revisar bundle, Git y logs |
| SSRF/proxy abierto | Host del proveedor fijo; paths/parámetros permitidos | P09: URL/host suministrado por cliente rechazado |
| Caché privada compartida | `private/no-store` en sesiones, ligas, saldo y pujas | P10: dos identidades no intercambian respuestas |
| Función SQL privilegiada | Preferir invoker; si definer, search_path fijo, nombres cualificados y EXECUTE restringido | Cada migración: llamada directa sin permiso falla |
| Exceso de proveedor | Contador compartido, tope, prioridades y reintentos limitados | P09: cuota agotada no inicia solicitudes |
| CI no confiable | Permisos mínimos y sin secretos de beta en PR externo | P02/P10: revisar triggers y permisos |

El limitador no depende únicamente de memoria de un Worker, que no es global ni persistente. En P04 se elegirá un mecanismo efectivo disponible gratis; cuotas críticas por usuario se podrán aplicar en una función transaccional con retención corta. Verificar disponibilidad y coste de cualquier capacidad específica del proveedor antes de usarla.

## Configuración y secretos

Variables públicas solo para configuración que deba conocer el navegador, como URL de Auth y clave publicable. La protección real de datos es RLS y permisos, no ocultar esa clave. Clave deportiva, clave de sistema y credenciales de despliegue son privadas y se separan por entorno.

`.env.example` contiene nombres y marcadores ficticios; archivos reales ignorados por Git. No pedir claves por chat. Las capturas y fixtures no incluyen cabeceras de autorización. Rotación si se filtra una clave; borrar un archivo del último commit no elimina exposición histórica.

## Privacidad y contenido

Antes de beta: definir responsable del tratamiento, datos mínimos, finalidad/base aplicable, destinatarios/proveedores, retención, canal de derechos y baja/exportación. Comprobar región y condiciones de tratamiento de los servicios elegidos; una región europea de BD no demuestra que todo tratamiento se quede en Europa. Usar información de la [AEPD sobre medidas de cumplimiento](https://www.aepd.es/derechos-y-deberes/cumple-tus-deberes/medidas-de-cumplimiento) para preparar la revisión aplicable al producto.

Perfil inicial propuesto: ID, alias y los datos de contacto estrictamente necesarios para el acceso. No pedir dirección, fecha de nacimiento ni teléfono por defecto. No instalar rastreadores publicitarios. Analítica inicial agregada a partir de eventos de juego, con retención acordada y sin IPs completas permanentes.

Describir cookies/almacenamiento realmente usados; si luego se introduce analítica no necesaria o publicidad, revisar los requisitos antes de activarla. Resolver menores, dinero real y países en D16. No presentar una plantilla de privacidad como validación jurídica terminada.

Fotos/escudos/licencias en registro de permisos; no hacer hotlink a la API para eludir derechos. Identidad propia sin afirmar afiliación oficial. Datos editoriales de disponibilidad distinguen fuente, certeza y caducidad.

## Pruebas proporcionales

- Unitarias: fórmula de puntos, redondeos, normalización, calendario y reglas puras. Casos esperados calculados independientemente.
- Integración real con PostgreSQL: dinero/propiedad, restricciones, RLS, funciones RPC, idempotencia, concurrencia y migraciones.
- UI: formularios, errores útiles, teclado y estados de carga; evitar snapshots masivos sin valor.
- E2E: dos usuarios completan el ciclo crítico; una tercera identidad no puede acceder. Añadir casos según cambie el comportamiento.
- Contrato de proveedor: fixtures saneados autorizados o sintéticos para campos ausentes, formato cambiado, paginación y error.
- Carga antes de beta: concurrencia del piloto y margen, medir latencias/errores/CPU/consultas; objetivo numérico tras primera medición. No deducir capacidad por la cuota MAU.

No añadir tests para retoques documentales o estilos triviales. Sí comprobar enlaces de documentación y visualmente el diseño cuando se implemente. Cada test responde a un riesgo observable.

## Entornos y despliegue

1. Local: datos sintéticos, BD/Auth locales cuando el equipo lo soporte.
2. CI: entorno efímero de prueba, sin datos reales ni claves deportivas.
3. Beta: proyecto separado, acceso por invitación y secretos propios; un solo entorno remoto al principio para no consumir cuotas innecesariamente.

Orden de despliegue: copia si afecta a datos → migración compatible → backend/frontend → smoke test de acceso, catálogo y lectura privada → habilitar funcionalidad. Migraciones destructivas requieren plan específico; preferir añadir, migrar y retirar en entregas separadas.

Rollback normal: volver al build anterior compatible. Una migración aplicada no se deshace a ciegas. Restaurar copia puede perder operaciones posteriores: detener escrituras, evaluar impacto y reconciliar antes de abrir otra vez.

## Copias y recuperación

Supabase recomienda exportaciones propias para proyectos Free; no dar por incluido un sistema de recuperación puntual. [Copias de Supabase](https://supabase.com/docs/guides/platform/backups).

Propuesta de piloto: copia diaria mientras haya juego y antes de cambios de esquema, cifrada y fuera del repositorio. Retención inicial propuesta de siete copias diarias y una previa a migración, ajustada a almacenamiento/derechos. Copias y manual en un destino bajo control del usuario. No es almacenamiento ilimitado ni una protección frente a perder el único equipo: resolver un segundo destino ya disponible antes de llamar al proceso «copia externa».

P10 debe comprobar qué incluye la exportación (esquemas de aplicación, identidades Auth, extensiones/funciones) y qué debe reconstruirse aparte (configuración OAuth, secretos, assets). Evitar asumir que un dump por defecto exporta todo. No hay assets oficiales almacenados inicialmente.

Objetivo propuesto y pendiente de ensayo: como máximo 24 horas de datos perdidos y recuperación en una sesión de trabajo. No prometerlo como SLA. Medir restauración en BD aislada, verificar miembros/saldos/propiedad/puntos y documentar tiempo real. Si un backup es manual, asignar responsable y frecuencia; no marcarlo automatizado.

## Manual de incidencias

| Incidencia | Respuesta inicial | Recuperación y evidencia |
| --- | --- | --- |
| Proveedor caído/cuota agotada | Conservar último dato válido y mostrar antigüedad | Reintento acotado tras recuperación; cursor y contadores |
| Dato deportivo incoherente | Cuarentena; no cerrar puntos afectados | Revisar fuente/revisión y recalcular con trazabilidad |
| Cierre de mercado interrumpido | Bloquear nuevas pujas por plazo, conservar estado | Reanudar trabajo idempotente; reconciliar libro y propiedad |
| Saldo/propiedad inconsistente | Pausar escrituras del ámbito afectado | Investigar, registrar reparación/contramovimiento y comprobar invariantes |
| BD gratuita pausada | Mostrar indisponibilidad; no simular confirmaciones | Reanudar según servicio, verificar trabajos vencidos y límites antes de procesar |
| Credencial expuesta | Revocar/rotar y limitar acciones | Revisar accesos/logs, sanear repositorio y documentar impacto |
| Despliegue defectuoso | Deshabilitar función o volver al build compatible | Smoke test y revisión de migración |
| Error de permisos | Cerrar acceso afectado y preservar evidencia | Corregir, probar acceso cruzado y evaluar datos expuestos |

## Observabilidad mínima

Logs estructurados con `requestId`, tipo de operación, duración, resultado y error sanitizado; nunca tokens, emails completos, pujas rivales ni payloads brutos. Registrar actor/ámbito en auditoría privada con retención definida.

Panel operativo: último trabajo correcto por recurso, datos pendientes/anómalos, antigüedad de estadísticas, cuota usada/restante, jobs fallidos, tamaño BD, errores HTTP y discrepancias contables. Alertas iniciales dentro del panel y revisión manual; no prometer email automático sin proveedor configurado.

## Lista de salida de beta

- [ ] Derechos y campos necesarios de datos reales verificados para el alcance.
- [ ] Reglas aprobadas y versión fijada para liga piloto.
- [ ] Auth real, recuperación de acceso y revocación probadas; sin dependencia accidental de SMTP de prueba.
- [ ] Acceso cruzado, RPC directo y roles probados.
- [ ] Concurrencia, doble envío e idempotencia de dinero/propiedad probados.
- [ ] Bloqueos temporales, correcciones y aplazamientos comprobados.
- [ ] Ningún secreto en bundle, Git, logs ni fixtures.
- [ ] Cuotas medidas, margen configurado y gasto 0 comprobado.
- [ ] Copia restaurada y procedimiento de caída probado.
- [ ] Privacidad, soporte, cierre de cuenta y audiencia D16 resueltos.
- [ ] Móvil, teclado, contraste y mensajes de error revisados.
- [ ] Responsable de revisar ingesta/mercado durante el piloto asignado.
