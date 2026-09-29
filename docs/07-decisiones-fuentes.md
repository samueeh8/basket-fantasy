# Decisiones, presupuesto y fuentes

Última consulta: 2026-09-29. Los precios y condiciones pueden cambiar; comprobar de nuevo antes de activar cada servicio. «0 €» significa sin gasto de servicios contratado, usando el equipo/conexión ya disponibles; no implica coste nulo de tiempo, electricidad ni futuras licencias.

## Registro técnico

| ID | Decisión | Estado | Motivo / condición para revisarla |
| --- | --- | --- | --- |
| A01 | Un backend modular, un repositorio y PostgreSQL | Seleccionada en el plan | Menos operación; separar servicios solo ante una necesidad medida |
| A02 | TypeScript + React/Vite + Hono/Workers | Seleccionada, verificar en P02/P10 | Compartir lenguaje y servir frontend estático; revisar si CPU gratuita no cabe |
| A03 | Supabase PostgreSQL/Auth, SQL y RLS | Seleccionada, verificar entorno local | Integridad relacional y acceso gestionado; exportable, Auth menos portable |
| A04 | Funciones transaccionales para dinero/propiedad | Seleccionada | Varias llamadas HTTP no son una transacción |
| A05 | UUID propios y mapas externos tipados | Seleccionada | Cambiar proveedor sin romper ligas |
| A06 | Datos sintéticos disponibles desde el inicio | Seleccionada | Desarrollo y CI independientes del proveedor y de la temporada |
| A07 | API-Basketball como candidato, no proveedor aprobado | Pendiente P01 | Acceso, completitud, frecuencia y uso sin certificar |
| A08 | Resultados diferidos inicialmente | Propuesta D17 | Cero presupuesto no permite prometer live |
| A09 | OAuth Google para beta | Propuesta D04 | Evitar depender de correo de prueba; requiere configurar y verificar proveedor |
| A10 | Una web responsive, sin app nativa inicial | Propuesta de alcance | Compartir acceso móvil/escritorio; confirmar D01 |
| A11 | Sin fotografías ni escudos oficiales inicialmente | Propuesta alineada con el brief | Recursos propios; reevaluar cuando existan permisos |
| A12 | Sin Redis, Kafka, Kubernetes, ML ni API de IA inicialmente | Seleccionada | No aportan al primer ciclo y añaden operación/coste |
| A13 | Sin Vercel Hobby como base comercial | Seleccionada | Restricción de uso personal no comercial del plan |
| A14 | Liga privada, local primero, temporada 2026/27 | Confirmada por usuario 2026-09-29 | URL se decidirá cuando haga falta; no cambiar temporada por facilidad del proveedor |
| A15 | Inicio con/sin plantilla y economía calibrada conjuntamente | Confirmada en alcance por usuario | Algoritmo, compensación, precios y saldo numérico pendientes; ver `08-reglas-economia.md` |
| A16 | TheSportsDB solo como alternativa parcial investigada | Evidencia limitada 2026-09-29 | Metadatos y cinco eventos recibidos; box scores/plantillas completas sin verificar |
| A17 | Jugador exclusivo dentro de cada liga | Confirmada por usuario 2026-09-29 | Único propietario activo por liga; la exclusividad no cruza ligas |
| A18 | Pujas secretas con contador visible | Confirmada por usuario 2026-09-29 | Mostrar número de pujas activas, incluida la propia; ocultar todos los postores e importes ajenos |
| A19 | Lote diario de varios jugadores; mayor puja gana al cierre | Confirmada por usuario 2026-09-29 | Número exacto, zona/hora, empates, presupuesto en varios triunfos y detalle publicado tras adjudicación se especifican en P06.1 |

Una decisión técnica seleccionada guía la implementación autorizada futura; no significa que se haya desplegado ni que el usuario haya respondido a las decisiones de producto. Si el usuario cambia una preferencia, actualizar este registro y sus consecuencias.

## Presupuesto inicial

| Componente | Coste previsto | Límite/condición | Qué hacer al acercarse al límite |
| --- | --- | --- | --- |
| Desarrollo local | 0 € de servicios | Equipo capaz de ejecutar stack; herramientas y licencias verificadas | Ajustar entorno antes de empezar |
| Frontend estático en Workers | 0 € | Assets servidos directamente; no enrutar todo por función sin necesidad | Revisar configuración y tamaño de build |
| API y cron Workers Free | 0 € | 100.000 requests/día; 10 ms CPU por request/cron; 5 cron triggers/cuenta según docs consultadas | Reducir trabajo por lote y medir; no activar Paid |
| Supabase Free | 0 € | 500 MB BD/proyecto; 5 GB egress; dos proyectos Free activos; pausa por baja actividad posible | Medir, paginar, depurar datos vencidos con copia y política |
| API deportiva Free | 0 € | 100 consultas/día; temporada y datos disponibles pendientes | Tope interno 80 propuesto; diferir/limitar funcionalidad |
| Subdominio del alojamiento | 0 € | URL proporcionada por servicio; identidad final pendiente | Mantener subdominio; no comprar dominio |
| Auth | Incluido en cuota | Método OAuth por confirmar; correo externo no resuelto | Verificar acceso real de amigos antes de beta |
| CI GitHub Actions | 0 € dentro de cuota | Minutos/almacenamiento según cuenta/repositorio y runner | Runner Linux estándar, artifacts breves, checks locales si se agota |
| Copias | 0 € si cabe en medios existentes | Destino/retención/responsable por concretar | Ajustar retención; no dejar copia única sin señalarlo |
| Fotos/licencias/live premium | No presupuestado | Fuera de alcance gratuito | Mantener recursos propios y funciones diferidas |

Son límites de servicios, no una estimación de capacidad de usuarios. No asumir que 50.000 usuarios de Auth caben en una BD de 500 MB con toda su actividad. No recomendar evadir cuotas mediante cuentas múltiples ni tráfico artificial para impedir pausas.

Umbrales internos propuestos: advertencia al 60 % de cuota/capacidad observada; revisión al 80 %; corte o degradación antes de superar el límite según recurso. A 0 € se sacrifica frecuencia o disponibilidad antes de generar gasto. Si los datos esenciales no están gratis, la versión ACB real a 0 € **no está garantizada**.

## Evidencias y límites de la investigación

| Fuente oficial | Qué respalda | Qué no demuestra |
| --- | --- | --- |
| [API-Sports Basketball](https://api-sports.io/sports/basketball) | ACB en catálogo; Free anunciado de 100 llamadas/día; planes de pago publicados | Campos completos, temporada Free actual o calidad medida |
| [Actualización de API-Basketball](https://www.api-football.com/news/post/api-basketball-new-release-available) | Endpoints individuales anunciados por el proveedor | Que cada campo esté disponible en ACB |
| [Documentación Basketball v1](https://api-sports.io/documentation/basketball/v1) | Referencia oficial para implementación futura | No se extrajo su contenido dinámico en esta revisión |
| [Condiciones API-Sports](https://api-sports.io/terms) | Condiciones de datos, visuales y cuotas | Una autorización específica para este proyecto |
| [TheSportsDB Free](https://www.thesportsdb.com/documentation) | API pública de prueba y límites por método | Cobertura suficiente del fantasy; solo se han observado metadatos ACB y cinco eventos 2026/27 |
| [Flashscore](https://www.flashscore.com/terms-of-use/) y [Sofascore](https://www.sofascore.com/de/terms-and-conditions) | Restricciones publicadas de uso comercial y extracción/scraping | Permiso específico para utilizar sus datos en este proyecto |
| [BALLDONTLIE NBA](https://docs.balldontlie.io/) | Producto NBA examinado | Cobertura ACB |
| [Precios Workers](https://developers.cloudflare.com/workers/platform/pricing/) | Existencia del nivel Free y facturación de funciones | Viabilidad de nuestro código sin medir |
| [Assets Workers](https://developers.cloudflare.com/workers/static-assets/billing-and-limitations/) | Peticiones estáticas gratuitas; diferencias al ejecutar Worker | Que SSR y backend sean ilimitados |
| [Límites Workers](https://developers.cloudflare.com/workers/platform/limits/) | CPU, solicitudes, conexiones, subrequests y cron | Garantía de ejecución puntual o capacidad fantasy |
| [React/Vite en Workers](https://developers.cloudflare.com/workers/framework-guides/web-apps/react/) | Ruta de integración soportada | Aplicación implementada |
| [Hono en Workers](https://hono.dev/docs/getting-started/cloudflare-workers) | Backend compatible | Seguridad automática del dominio fantasy |
| [Facturación Supabase](https://supabase.com/docs/guides/platform/billing-on-supabase) | Cuotas y proyectos de los planes | Capacidad real de este juego |
| [Pausa de proyectos](https://supabase.com/docs/guides/platform/free-project-pausing) | Posibilidad de pausa Free por baja actividad | Disponibilidad continua gratuita |
| [SMTP Supabase](https://supabase.com/docs/guides/auth/auth-smtp) | SMTP de prueba restringido a direcciones autorizadas y no destinado a producción | Email gratis funcionando para todos los amigos |
| [Desarrollo local Supabase](https://supabase.com/docs/guides/local-development) | CLI y stack local | Contenedores instalados en este equipo |
| [RLS](https://supabase.com/docs/guides/database/postgres/row-level-security) y [funciones SQL](https://supabase.com/docs/guides/database/functions) | Herramientas de permisos y lógica transaccional | Que nuestras futuras políticas sean correctas sin pruebas |
| [Backups Supabase](https://supabase.com/docs/guides/platform/backups) | Necesidad de definir exportación/restauración para Free | Recuperación puntual incluida para este MVP |
| [Vercel Hobby](https://vercel.com/docs/plans/hobby) | Restricción personal no comercial | Que cualquier prototipo privado sea automáticamente comercial o permitido |
| [GitHub Actions](https://docs.github.com/en/billing/concepts/product-billing/github-actions) | Cuotas y facturación por contexto | CI ilimitado en repositorio privado |
| [AEPD](https://www.aepd.es/derechos-y-deberes/cumple-tus-deberes/medidas-de-cumplimiento) | Marco de medidas para tratamiento de datos personales | Revisión jurídica final de la aplicación |

No se han revalidado la fecha de lanzamiento de estadísticas avanzadas ACB citada en el chat, el número exacto de métricas nuevas, precios de Sportradar ni ninguna posible colaboración comercial. No son dependencias del MVP ni hechos que el proyecto deba anunciar.

## Cómo registrar una decisión nueva

Añadir ID, fecha, estado (propuesta/aceptada/sustituida), problema, opciones consideradas, decisión, evidencia, efecto en presupuesto y entregas afectadas. Vincular la respuesta del usuario cuando se trate de reglas. No borrar el motivo de decisiones sustituidas: indicar cuál las reemplaza.
