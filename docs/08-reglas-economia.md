# Reglas y calibración económica

Estado: requisitos parciales confirmados el 2026-09-29; todavía no hay fórmula de precios ni puntos aprobada. Este documento desarrolla D06–D14 y D19 sin decidirlos por el usuario.

## Confirmado

- Liga privada, desarrollo local, temporada ACB 2026/27.
- Al crear una liga se elige comenzar con plantilla o sin plantilla.
- Jugadores exclusivos dentro de cada liga: un jugador activo pertenece a un solo manager de esa liga, aunque puede pertenecer a managers distintos en otras ligas.
- Mercado por pujas secretas. La pantalla publica cuántas pujas activas tiene un jugador; no publica quién pujó ni ningún importe. Cada manager ve únicamente su propia puja.
- El sistema ofrece varios jugadores al día y adjudica cada jugador al cierre diario a la puja de mayor importe.
- El saldo inicial debe calibrarse con precios y funcionamiento del mercado.
- Se estudiarán tres alternativas de puntuación: nota sobre 10, valoración y fórmula propia. Esto no significa implementar tres modos desde el MVP.

## Exclusividad por liga

Ejemplo: si un manager tiene a Campazzo en la liga Amigos, otro miembro de Amigos necesitaría adquirirlo a ese manager para incorporarlo. En la liga Oficina podría tenerlo otra persona. La propiedad activa se fuerza mediante una restricción de base de datos ligada a la liga, no mediante una comprobación visual.

## Mercado: precisar antes de implementarlo

El sistema publica un lote de varios jugadores al día. Las pujas permanecen secretas durante la ventana; al cierre diario se adjudica cada jugador a quien haya ofrecido el importe más alto. El listado muestra `N pujas`, donde N cuenta pujas activas distintas e incluye la del visitante. El manager consulta su propia puja; la identidad e importe de las ofertas rivales no se muestran. Una adjudicación actualiza la plantilla del ganador sin desvelar el importe ni la identidad de quienes pujaron.

Siguen por concretar: número de jugadores del lote, hora/zona horaria y límites exactos de apertura/cierre, tratamiento de pujas empatadas, saldo reservado y validez de pujas si varias victorias exceden el presupuesto, mínimo de puja, cambios/retiros antes del cierre, venta al sistema, ofertas entre managers, saldo negativo y actualización del valor. Pedir decisiones por bloques, no toda la lista a la vez.

## Primero valores y después presupuesto

Protocolo de calibración propuesto para P05.0:

1. Fijar número de participantes, tamaño de plantilla y requisitos de posiciones. Medir cuántos jugadores elegibles existen por posición; si hay exclusividad, comprobar que oferta y demanda permiten completar equipos.
2. Decidir qué significa el valor base: rendimiento esperado, escalas por rangos u otro criterio. Si depende de la puntuación, resolver primero una fórmula candidata. Distinguir valor base de precio realmente pagado y de valor de reventa.
3. Elegir las entradas disponibles, su periodo y tratamiento de debutantes, lesiones o muestra escasa. Históricos pueden ayudar a inicializar precios sin sustituir la temporada 2026/27 de juego; necesitan acceso y calidad propios.
4. Construir distribución de precios iniciales sin comprometer importes definitivos: mínimos, medianas, máximos, precio por posición y coste de varias plantillas legales.
5. Simular managers con estrategias distintas, ambos modos de inicio y varios tamaños de liga. Observar porcentaje de plantillas completables, concentración de jugadores caros, saldo ocioso, jugadores sin comprador e inflación después de jornadas simuladas.
6. Derivar un saldo candidato del coste de plantilla objetivo más margen para competir en pujas. Elegir ese margen y la generosidad del inicio con el usuario; no fijar una cifra arbitraria.
7. Comparar modo con plantilla: propuesta para evaluar, `patrimonio inicial = valor de jugadores asignados + efectivo`. Decidir si igualar patrimonio entre managers/modalidades, usar bandas de tolerancia o admitir otra regla. No asumir descuento automático del valor de plantilla.
8. Documentar resultados, elegir configuración inicial y guardarla en una versión de reglas. Repetir simulación si cambian tamaño, escasez o actualización de precios.

Los datos sintéticos permiten validar la mecánica; la calibración orientada a jugadores ACB debe contrastarse después con datos reales. No presentar los precios sintéticos como valores de mercado reales. La simulación no garantiza diversión ni equilibrio: se revisa tras la beta.

## Puntuación: alternativas y datos necesarios

| Candidata | Decisiones pendientes | Ventajas / implicaciones de diseño |
| --- | --- | --- |
| Nota sobre 10 | Escala mínima, transformación, redondeo, no jugó y valores extremos | Lectura familiar; hay que definir el cálculo subyacente y comprobar que la compresión no elimina diferencias relevantes |
| Valoración | Fuente exacta, disponibilidad o términos para reconstruirla | Base explicable si está disponible; no todas las métricas llamadas valoración son equivalentes |
| Fórmula propia | Pesos de acciones, resultado y sanciones, precisión y reglas de acumulación | Más control; requiere calibración y desglose visible para que el usuario entienda los puntos |

Para una fórmula propia: enumerar cada término, su origen y qué premia/castiga. Si se parte de una valoración compuesta, verificar qué incorpora antes de sumar tiros, fallos, faltas u otras acciones; una doble ponderación solo debe existir si se decide expresamente.

Victoria/derrota: decidir si aplica a todos los jugadores del club, solo participantes o con un umbral de minutos, y si es suma fija o porcentaje. Evitar premiar a quien no jugó por accidente.

Técnicas/antideportivas/expulsiones: exigir eventos o campos identificables, diferenciar jugador y banquillo/entrenador, definir si sanciones acumuladas y expulsión suman penalizaciones. Una falta personal total no demuestra una técnica; una expulsión no se infiere de minutos bajos. Dato ausente no significa cero sanciones.

## Ensayo de la fórmula

- Seleccionar casos variados: gran anotador poco eficiente, jugador defensivo, suplente eficiente, rendimiento negativo, prórroga, no jugó y sanciones.
- Calcular resultados independientes a mano y con el motor; mostrar desglose.
- Comparar distribución de puntos por posición y minutos; discutir si refleja el tipo de juego deseado.
- Probar efecto de victoria/derrota y sanciones de forma aislada.
- Escoger una versión inicial, publicar reglas y congelarla para la liga piloto. No modificar puntos retroactivos sin política aprobada.

No seleccionar todavía pesos ni nota mínima. La primera auditoría debe decir qué componentes son viables con datos gratuitos de 2026/27.
