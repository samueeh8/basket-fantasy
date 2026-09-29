# Estado y continuidad

Actualización: 2026-09-30. Fase actual: **P02 · base local reproducible**.

## Hechos comprobados

- La carpeta inicial solo contenía `.git`; no había código ni instrucciones locales AGENTS.md en los directorios inspeccionados.
- Se ha preparado el mapa técnico y de producto, con preguntas abiertas y fuentes oficiales.
- El usuario confirmó liga privada, desarrollo local y temporada 2026/27; inicio con/sin plantilla seleccionable y saldo a calibrar con mercado/precios.
- No se ha llamado a la API deportiva con una clave, ni medido cobertura real de ACB.
- Precisión: lo anterior se refiere a API-Basketball y una clave privada. Sí se realizaron dos GET públicos a TheSportsDB Free: metadatos ACB 2026/27 y cinco eventos de esa temporada. No se verificaron plantillas completas ni estadísticas individuales.
- Inventario del equipo: Node.js v22.16.0 y npm 11.5.2 disponibles; Git disponible; Docker y Supabase CLI no encontrados. El ejecutable de WSL está presente, pero todavía no se ha comprobado que la distribución esté lista para contenedores.
- No se han instalado dependencias, creado cuentas, contratado servicios, desplegado ni enviado mensajes.

## Tablero

| Pipeline | Estado | Dependencia pendiente |
| --- | --- | --- |
| P00 Alcance y reglas iniciales | EN DEFINICIÓN | D01–D03, D06 y mecánica base de D09 respondidas; hora, empates y saldo antes de P06 |
| P01 Auditoría del proveedor | EN CURSO | Investigación pública y muestra TheSportsDB realizadas; falta clave privada API-Sports para prueba completa |
| P02 Base local | EN CURSO | P02.1 confirmó Node/npm/Git; Docker falta para Supabase local. P02.2 (web + API de salud) puede empezar sin BD; resolver motor de contenedores antes de P02.3 |
| P03 Catálogo | PENDIENTE | P02 |
| P04 Usuarios y ligas | PENDIENTE | P03 y D04–D05 |
| P05 Plantillas y saldo | PENDIENTE | P04 y D06–D08 |
| P06 Mercado | PENDIENTE | P05 y D09–D11 |
| P07 Alineaciones | PENDIENTE | P06 y D12–D13 |
| P08 Puntuación | PENDIENTE | P07 y D14–D15 |
| P09 Datos reales | PENDIENTE | P01 con resultado favorable + P08 |
| P10 Alojamiento | PENDIENTE | P08; se puede ensayar antes con catálogo sintético |
| P11 Beta | PENDIENTE | P09, P10, seguridad y D16–D18 |
| P12 Evolución | FUTURO | Evidencia de uso de P11 |

Estados permitidos: PENDIENTE, EN DEFINICIÓN, LISTO, EN CURSO, BLOQUEADO, HECHO, FUTURO. HECHO requiere todos los criterios de aceptación de la tarea y evidencia registrada.

## Siguiente paso exacto

1. Completar P01.1: crear cuenta directa Free de API-Sports, guardar clave como `API_SPORTS_KEY` en `.env.local` (ignorado por Git) y comprobar catálogo/temporada **2026/27**. Nunca pegar la clave en el chat.
2. API-Basketball es la primera candidata, no un proveedor aprobado; TheSportsDB queda como alternativa parcial investigada. Ver `04-auditoria-proveedor.md`.
3. Primer paso de desarrollo: P02.2, crear una web mínima React/Vite y una API Hono con `/api/health`; mostrar en la pantalla si la API responde. La prueba local no necesita datos ACB ni base de datos.
4. Después resolver Docker/WSL para P02.3 (Supabase local) antes de modelar ligas persistentes. No instalar componentes del sistema sin revisar el equipo.

## Bloqueos y rutas para seguir

| Bloqueo | Efecto | Trabajo independiente disponible |
| --- | --- | --- |
| Falta de clave deportiva | No se puede certificar cobertura ni cuotas observadas | Catálogo sintético, interfaz, autenticación y arquitectura |
| Temporada actual no incluida en Free | No hay garantía de MVP real a 0 € | Demo sintética/histórico permitido; investigar otro proveedor sin cambiar objetivo |
| Derechos de publicación no aclarados | No abrir beta real con esos datos | Desarrollo sintético y documentación de consulta al proveedor |
| Reglas no decididas | No implementar el módulo dependiente | Infraestructura, diseño y módulos independientes |
| Límite gratuito insuficiente | No ampliar gasto automáticamente | Reducir frecuencia/alcance, optimizar o mantener entorno local |

## Registro de sesiones

| Fecha | Resultado | Verificación | Próximo paso |
| --- | --- | --- | --- |
| 2026-09-29 | Arquitectura, mapa y preguntas documentados | Inspección inicial, fuentes oficiales y verificación de enlaces locales/bloques Markdown de 11 documentos; sin pruebas de aplicación | Resolver D01–D03 y comenzar P01.1/P02.1 |
| 2026-09-29, actualización | Lote diario de mercado y adjudicación al mayor importe al cierre confirmados | Reglas propagadas a producto, datos, seguridad y pipelines; detalles de hora/empate/saldo pendientes | Clave Free local para P01.1; detallar esos bordes antes de implementar P06 |
| 2026-09-30 | Inventario inicial de herramientas locales | Node 22.16.0, npm 11.5.2 y Git disponibles; Docker/Supabase CLI no encontrados | P02.2 web + API mínima; comprobar motor de contenedores antes de P02.3 |

Las preguntas iniciales y las aclaraciones principales de mercado están respondidas. P06.1 concretará hora/zona de cierre, empates, saldo cuando un manager gane varias pujas y cambios/retiros; no impedirá avanzar antes con base de datos y catálogo sintéticos.

## Cómo retomar

Petición útil: «Lee el estado del proyecto y vamos con la siguiente tarea lista de Pxx». Al terminar, registrar los archivos y pruebas relevantes aquí; el historial detallado de cambios vivirá también en Git.
