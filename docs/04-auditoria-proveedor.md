# Auditoría de API-Basketball para ACB

Estado: **API-Basketball pendiente de consultas autenticadas**; comprobación pública limitada realizada con TheSportsDB. Temporada objetivo confirmada: **2026/27**. Esta página es el protocolo y la matriz inicial, no un informe de cobertura aprobada. No hay muestras deportivas almacenadas en el repositorio.

## Qué se ha verificado públicamente

La página del proveedor incluye ACB en su cobertura y anuncia un plan Free de 100 peticiones al día. Eso no acredita cada campo, temporada o frecuencia. [Cobertura y planes](https://api-sports.io/sports/basketball).

Su anuncio de actualización documenta endpoints de jugadores y estadísticas individuales. La documentación interactiva no devolvió contenido legible en esta revisión; los parámetros y esquemas se deben confirmar antes de programar el cliente. No confundir Basketball con la API NBA del mismo proveedor. [Anuncio oficial](https://www.api-football.com/news/post/api-basketball-new-release-available), [documentación Basketball v1](https://api-sports.io/documentation/basketball/v1).

Las condiciones distinguen acceso técnico de derechos de publicación; mencionan posibles licencias adicionales para fantasy y recursos visuales de terceros. Por ello, datos y recursos gráficos tendrán verificaciones separadas antes de su publicación. [Condiciones](https://api-sports.io/terms).

## Dos resultados independientes

- **Técnico:** APTO / APTO CON LIMITACIONES / NO APTO / SIN EVIDENCIA.
- **Uso:** ACLARADO PARA EL ÁMBITO / PENDIENTE / NO PERMITIDO.

Un resultado técnico favorable no cambia el estado de uso. La beta real exige ambas puertas resueltas; el prototipo sintético no depende de ellas.

## Procedimiento paso a paso

1. Usar D03: temporada 2026/27 confirmada; concretar fases. Registrar proveedor, producto, plan, fecha y límites que ve la cuenta.
2. Guardar clave exclusivamente en configuración local ignorada por Git. Usar suscripción directa Free si mantiene corte de cuota; no activar cobros por exceso.
3. Consultar estado y catálogo de competiciones, verificar ACB por país/nombre y temporadas. No copiar un ID encontrado en un ejemplo como si fuese el correcto.
4. Verificar acceso real Free a la temporada elegida. Distinguir permiso denegado, consulta mal formada, ausencia de partido y respuesta vacía.
5. Traer equipos y todas las páginas de jugadores/plantillas. Registrar tamaños, nulos, duplicados, bajas y cambios de club.
6. Descargar una muestra pequeña de calendario y partidos terminados. Ampliar progresivamente a todos los clubes en al menos dos jornadas si hay datos y cuota; incluir prórroga/aplazado cuando existan.
7. Comparar manualmente una muestra de resultados/estadísticas con actas o fuentes de referencia consultables, anotando URL y fecha. No montar un scraper ni redistribuir esas fuentes como fallback.
8. Repetir consultas en días distintos y tras partidos; medir demora hasta disponibilidad y hasta corrección. Para live, solo muestrear si el presupuesto lo permite; no prometer una frecuencia por la documentación.
9. Probar importación repetida, respuesta incompleta, timeout, 429, cambio de formato e ID desconocido con fixtures sintéticos cuando no convenga gastar llamadas.
10. Registrar consumo total con paginación, reintentos, consultas de estado y correcciones. Modelar semana normal y concentración de partidos.
11. Preparar consulta de derechos: publicación en fantasy comercial, beta privada, conservación/cache, datos derivados, atribución, territorios y visuales. Guardar respuesta escrita si se obtiene. No enviar nada sin instrucción explícita.
12. Redactar conclusión con campos utilizables, fórmula fantasy viable, frecuencia conseguible, limitaciones y alternativa. No completar casillas con suposiciones.

## Matriz inicial

Leyenda: NC = no comprobado mediante respuesta real ACB. La frecuencia de todas las filas deportivas está **sin medir**. En uso, D = requiere aclarar ámbito de datos; V = autorización de recurso visual; E = revisión editorial/fuente.

| Dato | Disponible ACB | Calidad que medir | Frecuencia a comprobar | Derechos | Alternativa si falta |
| --- | --- | --- | --- | --- | --- |
| Competición/temporada Free | NC; catálogo público incluye ACB | Temporada/fase y alcance exactos | Cambios de temporada | D | Demo sintética; evaluar otra fuente |
| Equipos/IDs | NC | Clubes completos, IDs estables | Altas/cambios | D | Carga autorizada y trazada |
| Jugadores/IDs | NC | Duplicados, homónimos, continuidad | Altas y traspasos | D | Reconciliación manual con fuente permitida |
| Plantillas reales | NC | Todos los inscritos, no solo quienes jugaron | Altas/bajas | D | No activar jugador incompleto; revisión |
| Posición | NC | Taxonomía, nulos, múltiples posiciones | Cambios | D | Posición de juego editorial solo si se decide |
| Altura/nacionalidad/dorsal | NC | Unidades, nulos y vigencia | Cambios | D | Omitir campos opcionales |
| Calendario/jornada/estado | NC | UTC, aplazados, cancelados y fase | Reprogramaciones | D | Ajuste administrativo documentado |
| Resultado y parciales | NC | Marcador final/prórroga | Tras partido y correcciones | D | Mantener pendiente hasta fuente válida |
| Minutos | NC | Formato, segundos, no jugó vs ausente | Tras partido | D | Excluir de fórmula si no fiable |
| Puntos | NC | Completitud por jugador/partido | Tras partido | D | No publicar puntuación incompleta |
| Rebotes ofensivos/defensivos/total | NC | Desglose y coherencia | Tras partido | D | Usar total si fórmula aprobada lo admite |
| Asistencias | NC | Nulos y rectificaciones | Tras partido | D | Cambiar fórmula antes de iniciar liga |
| Robos/tapones/pérdidas | NC | Cada campo y su semántica | Tras partido | D | Excluir campo no fiable con decisión |
| Tiros de 2, 3 y libres | NC | Intentos/aciertos, desglose | Tras partido | D | Derivar solo si hay entradas suficientes |
| Faltas cometidas/recibidas | NC | Son campos distintos | Tras partido | D | No asumir valoración ACB |
| Técnicas/antideportivas/descalificantes | NC | Tipo, sujeto sancionado y vínculo a jugador; no inferir del total de faltas | Tras partido/correcciones | D | Desactivar componente no disponible o revisión editorial explícita |
| Expulsiones | NC | Motivo y relación con sanciones previas; evitar penalización duplicada involuntaria | Tras partido/correcciones | D | No inferir expulsión de falta de minutos |
| Valoración del jugador | NC | Valor reportado o todos los términos para reconstruirlo; semántica exacta | Tras partido/correcciones | D | Fórmula propia documentada |
| Tapones recibidos | NC | Existencia y cobertura | Tras partido | D | Fórmula propia sin ese término |
| Titularidad | NC | Booleano explícito y cobertura | Tras partido | D | Omitir bonus dependiente |
| Live individual | NC | Latencia, parciales, cobertura real | Medición con cuota | D | Resultados diferidos |
| Fotos | NC | URL, identidad, vigencia | Cambios | V | Avatar propio genérico |
| Escudos | NC | Recurso y titular | Cambios | V | Nombre/abreviatura e identidad propia |
| Lesiones/disponibilidad | NC | Fuente, hora, grado de certeza | Editorial | E | No mostrar o edición trazable posterior |
| Noticias | NC | Enlace, autor, permisos de extractos | Editorial | E | Enlaces propios seleccionados después |
| Métricas avanzadas | NC | Fórmula, entradas, comparabilidad | Tras partido | D | Derivadas propias documentadas |

## Presupuesto de consultas

Fórmula: `total diario = catálogo + calendario + estadísticas + paginación + comprobaciones + reintentos + correcciones`.

Ejemplo puramente de planificación: 5 llamadas de catálogo/calendario + 9 partidos × 2 llamadas estadísticas + 9 de revisión + 8 de estado/reintentos = 40. No es una medición de la API ni una garantía: si exige consultar cada jugador o más páginas, puede no caber.

Política propuesta: tope interno configurable de 80 llamadas diarias en una cuenta Free de 100, contando toda ejecución; mantener margen para incidencias. Compartir contador atómico entre trabajos, contar conservadoramente intentos fallidos y registrar uso externo observado. En el panel directo el periodo se reinicia en UTC; confirmar cabeceras y plan real. Si no conocemos el remanente, no iniciar un lote que pueda consumirlo entero. [Cuotas y canal de contratación](https://api-sports.io/terms).

Orden de prioridad: calendario que afecta a bloqueos, estadísticas finales pendientes, correcciones recientes, plantillas, datos opcionales. Nada de polling deportivo por visitante. Las importaciones iniciales grandes se reparten entre días.

## Criterios propuestos para declarar APTO

- Temporada objetivo realmente accesible y todos sus equipos reconciliados.
- Identidad interna asignable sin colisiones; las ambigüedades se detectan y revisan.
- Plantillas suficientemente completas para los jugadores que se oferten; no prometer completitud por haber visto solo box scores.
- Todos los campos obligatorios de la fórmula elegida presentes en la muestra aceptada; registrar tamaño y sesgos de muestra. La muestra no garantiza cobertura futura.
- Latencia medida compatible con D17 y correcciones reproducibles.
- Consumo calculado con margen y protección efectiva de cuota.
- Ingesta repetida sin duplicados; fallos no destruyen la última versión válida.
- Evidencia de ámbito de uso archivada antes de publicar datos reales.

Si falla: omitir campos opcionales, ajustar fórmula solo con decisión explícita, evaluar otra fuente o mantener demo sintética. Subir a Pro no es una solución dentro del presupuesto autorizado.

## Formato de evidencia

Cada hallazgo: ID, fecha/hora UTC, endpoint y parámetros sin clave, temporada, estado HTTP, resultado, número de páginas, completitud, cuota, retardo observado y decisión. Evidencias locales sensibles fuera de Git. Crear `docs/auditorias/AAAA-MM-DD-acb.md` al ejecutar la auditoría, enlazarla desde el estado y actualizar esta matriz.

## Investigación de alternativas · 2026-09-29

| Fuente | Evidencia disponible | Decisión de trabajo |
| --- | --- | --- |
| API-Basketball / API-Sports | Catálogo ACB y Free de 100 solicitudes/día publicados; sin clave ni respuesta ACB 2026/27 de nuestra cuenta | Primera candidata para auditoría completa; no asegurar ni negar aún acceso Free a 2026/27 |
| TheSportsDB Free v1 | Dos consultas públicas realizadas: identifica liga 4408 como Spanish Liga ACB, temporada actual 2026-2027; consulta de temporada devuelve cinco eventos de 2026-2027 | Candidata auxiliar para calendario/metadatos; no acredita todas las jornadas, plantillas ni box scores individuales |
| BALLDONTLIE NBA | La documentación examinada corresponde a NBA | No usar esa API como prueba de cobertura ACB; no sustituir competición |
| Flashscore | Condiciones 2.2, 2.9 y 2.10 restringen uso comercial, extracción y scraping sin consentimiento, salvo excepciones aplicables | No seleccionada como fuente automática del proyecto con la evidencia actual |
| Sofascore | Condiciones 2.2, 2.8 y 2.9 contienen restricciones de uso comercial, extracción y scraping | No confundir endpoints internos accesibles con API pública licenciada |
| Importación local de archivos | Alternativa técnica propia, sin proveedor contratado | Admitir JSON/CSV de datos con procedencia y uso comprobados; automatización del importador no resuelve derechos del origen |

Fuentes: [API-Basketball](https://api-sports.io/sports/basketball), [TheSportsDB](https://www.thesportsdb.com/documentation), [BALLDONTLIE NBA](https://docs.balldontlie.io/), [Flashscore](https://www.flashscore.com/terms-of-use/), [Sofascore](https://www.sofascore.com/de/terms-and-conditions). Se consultó la ruta localizada de Sofascore porque la raíz devolvía solo navegación; contiene las condiciones en inglés. No se ha concluido que todo scraping sea ilegal ni que esta lista agote todos los proveedores.

Prueba TheSportsDB realizada mediante GET, sin cuenta ni clave privada, usando la clave pública de prueba documentada `123`:

- `lookupleague.php?id=4408`: `strLeague=Spanish Liga ACB`, `strSport=Basketball`, `strCurrentSeason=2026-2027`.
- `eventsseason.php?id=4408&s=2026-2027`: cinco eventos, todos con `strSeason=2026-2027`.
- Base: `https://www.thesportsdb.com/api/v1/json/123/`. No se han guardado payloads ni descargado imágenes. Cinco eventos no prueban completitud: comprobar límites de respuesta antes de usarlos como calendario.

La documentación de TheSportsDB publica restricciones importantes por método para el acceso Free. No basta con que exista un endpoint llamado estadísticas: hace falta una muestra ACB por jugador/partido con nuestros campos. No se ha validado esa muestra.

Conclusión actual: **hay acceso gratuito probado a algunos metadatos/calendario 2026/27, pero no hay aún un proveedor gratuito validado para el fantasy completo**. Próximo paso: cuenta directa Free de API-Sports y consultas auditadas. No utilizar las restricciones de temporada de API-Football o la cobertura de API-NBA para inferir las de API-Basketball.

## Si la API candidata no sirve

1. Registrar exactamente si falla precio/temporada, campos, cuota o permiso; no confundir una respuesta vacía de un partido futuro con falta de cobertura.
2. Evaluar una segunda fuente contra los mismos campos críticos, manteniendo IDs propios y procedencia por registro.
3. Para probar un ciclo local, habilitar importación pequeña de JSON/CSV con datos reales obtenidos de una fuente utilizable, o sintéticos identificados mientras no se disponga de ella. No dar la importación manual por exenta de condiciones.
4. Si se estudia scraping, escoger primero fuente/páginas, revisar condiciones, acceso y volumen, y medir estabilidad con una muestra. Respetar límites y no eludir login, CAPTCHA, bloqueos ni pagos. La autorización del usuario para investigar esta vía queda registrada; no necesita volverse a pedir solo por ser scraping.
5. Una fuente sin permiso aclarado o sin fiabilidad no se convierte automáticamente en dependencia de la beta comercial. Mantener desarrollo local independiente del adaptador.
