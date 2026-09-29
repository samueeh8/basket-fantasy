# Instrucciones de continuidad

## Antes de trabajar

- Leer `docs/00-estado.md`, `docs/01-producto.md` y la entrega correspondiente de `docs/05-pipelines.md`.
- Consultar arquitectura, modelo de datos y seguridad cuando el cambio afecte a esas áreas.
- Revisar el estado de Git y preservar cambios ajenos.
- La documentación describe el destino; no asumir que algo está implementado sin comprobarlo.

## Límites y decisiones

- Presupuesto de servicios: 0 €. No activar planes de pago, pruebas con cobro posterior ni recursos facturables sin instrucción explícita del usuario.
- No inventar reglas de juego. Consultar los identificadores Dxx en `docs/01-producto.md`; una propuesta no equivale a una decisión aceptada.
- No usar datos, fotografías, escudos ni marcas del proveedor como si su presencia en una API probase autorización de uso. Consultar la auditoría.
- Se puede seguir desarrollando con datos sintéticos claramente identificados mientras una integración esté bloqueada.
- No enviar mensajes a proveedores ni a terceros sin autorización explícita.
- No extraer ACB.com automáticamente como sustituto del proveedor.
- El usuario ha autorizado estudiar scraping de Flashscore/Sofascore u otra fuente como alternativa si no hay API gratuita suficiente. Evaluar acceso, términos, estabilidad y volumen; esa autorización no prueba permiso de terceros. No volver a pedir autorización solo para investigar esta vía, ni eludir bloqueos o controles de acceso.
- Alcance confirmado: liga privada, local primero, temporada 2026/27. Inicio con/sin plantilla configurable; presupuesto a calibrar con precios/mercado. Consultar `docs/08-reglas-economia.md` antes de fijar importes o puntuación.
- No abrir frentes de funcionalidades posteriores para evitar una decisión pendiente del paso actual.

## Forma de avanzar

- Trabajar una tarea pequeña y demostrable cada vez; usar `docs/plantillas/tarea.md` cuando empiece implementación.
- Cada función incluye interfaz, autorización, validación, persistencia y pruebas proporcionales.
- Los saldos, adjudicaciones, bloqueos y puntuaciones son autoridad del servidor; transacciones e idempotencia para operaciones críticas.
- Cada migración incluye restricciones y permisos desde el inicio. Probar con usuarios de ligas diferentes.
- Las credenciales no van en Git, capturas, ejemplos, fixtures ni registros.
- No añadir infraestructura nueva sin justificar necesidad, coste y efecto en operación.
- Al terminar actualizar `docs/00-estado.md`: entrega, cambios, comprobaciones ejecutadas, limitaciones y siguiente tarea exacta.
- Registrar decisiones nuevas en `docs/07-decisiones-fuentes.md` y respuestas de producto en `docs/01-producto.md`.
- Marcar una tarea como terminada solo con evidencia. Un diseño escrito no es una función implementada.

## Cierre de cada sesión

Indicar qué funciona, cómo se comprobó, qué queda pendiente y qué tarea permite retomar. No marcar el proyecto completo por haber terminado su documentación.
