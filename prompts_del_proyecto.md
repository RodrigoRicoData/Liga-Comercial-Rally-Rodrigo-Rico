# Prompts del proyecto

## 1. Prompt de producción (dentro del workflow de n8n)

Este es el prompt que el nodo HTTP envía a la API de Claude cada lunes, junto con los datos calculados del rally:

```
Sos el analista comercial de una cervecería en Santa Cruz, Bolivia. Con los
datos del rally de apertura de nuevos clientes que te paso en JSON, redactá
un resumen ejecutivo BREVE (máximo 200 palabras) en español para el jefe de
ventas: 1) top 3 del ranking, 2) avance vs meta trimestral de 250 puntos,
3) las alertas de puntos sin recompra con una acción sugerida para cada una,
4) la zona más rezagada. Tono directo y accionable. Solo sugerís: la decisión
final es del jefe de ventas.

Datos: {JSON con ranking, alertas y totales}
```

**Decisiones de diseño del prompt:**
- Se fija un **rol** (analista comercial) y un **contexto local** (Santa Cruz, Bolivia) para que el tono sea el correcto.
- Se limita la **extensión** (200 palabras): el jefe de ventas lo lee desde el celular.
- Se pide **estructura explícita** (4 puntos) para que el email sea consistente semana a semana.
- Se deja **explícito el límite de la IA**: sugiere acciones, no las decide. El control queda en la persona.

## 2. Prompts de desarrollo (metodología de trabajo con IA)

Durante el armado del proyecto se trabajó con Claude como asistente de diseño. Los prompts principales fueron:

**a. Encuadre inicial** — se le pasó el prototipo HTML y el contexto del negocio pidiéndole que hiciera preguntas antes de proponer, en lugar de asumir:

> "Eres un experto en prompt engineering, te pasaré el contexto de lo que queremos y el prototipo que ya tenemos [...] quiero que leas el documento y me hagas preguntas para que te dé un mejor contexto. La idea es automatizar el seguimiento de apertura de nuevos clientes en la cervecería, actualmente este seguimiento se lo hace de manera manual en Excel [...]"

**b. Diagnóstico del "antes"** — a partir de las preguntas de la IA se precisó que el proceso original ni siquiera existía de forma estable: el rally se activaba esporádicamente con un Excel de dos columnas (vendedor / cantidad de puntos), sin validación ni seguimiento.

**c. Decisiones tomadas por el autor (no por la IA):**
- Elegir n8n como herramienta de automatización.
- Simplificar el flujo a un solo workflow (resumen semanal por email) en lugar de una arquitectura de múltiples escenarios que la IA había propuesto inicialmente.
- Definir las reglas de negocio del rally: mínimo Bs 300, 20 pts por apertura, 35 pts por recompra, validación del supervisor en 48 h.
- Mantener el premio a la recompra por encima del premio a la apertura, para corregir el incentivo del proceso original (que premiaba solo cantidad).

**d. Qué salió mal y cómo se corrigió:** la primera propuesta de la IA era demasiado compleja (webhooks de registro, validación automatizada, mapas en vivo). Se la redirigió hacia un flujo mínimo viable que demuestre la transformación del proceso sin fricción técnica innecesaria — coherente con la regla de oro de la diplomatura: primero un proceso simple y claro, después la sofisticación.
