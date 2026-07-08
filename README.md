# 🍺 Liga Comercial · Rally de Apertura de Nuevos Clientes

**Trabajo Final Integrador · Diplomatura en Diseño de Procesos de Negocios con Plataformas Visuales de Automatización e IA Agéntica · FCE-UBA · Cohorte 2026**

> Elegí este proceso porque el seguimiento de apertura de nuevos clientes en una cervecería de Santa Cruz (Bolivia) se hace hoy de manera improvisada: cuando el jefe de ventas activa un "rally", anota en un Excel básico el nombre del vendedor y la cantidad de puntos que abrió, y al final premia al que más abrió. No hay validación, no hay seguimiento de recompra, no hay visibilidad durante la competencia y no queda ningún dato aprovechable.

### 🔗 [Ver la maqueta en vivo](https://rodrigoricodata.github.io/Liga-Comercial-Rally-Rodrigo-Rico/liga_comercial_rally.html)

## ¿Qué transforma este proyecto?

Convierte ese Excel improvisado en una **liga comercial gamificada con seguimiento automatizado**:

- Cada vendedor registra el punto nuevo desde el celular con **foto, ubicación GPS, canal y monto del primer pedido**.
- El punto solo es válido si el pedido inicial es **≥ Bs 300** y el **supervisor lo valida en 48 horas** (control humano).
- Un ranking con índice general premia no solo abrir puntos, sino que **vuelvan a comprar**: `índice = aperturas × 20 + recompras × 35 + ventas ÷ 30`.
- Cada lunes, un workflow de **n8n** lee los datos, calcula el ranking y las alertas (puntos con +15 días sin recompra), **Claude redacta un resumen ejecutivo** y se lo **envía por email al jefe de ventas** con el enlace al dashboard.

## Estructura del repositorio

| Archivo | Contenido |
|---|---|
| [`liga_comercial_rally.html`](https://rodrigoricodata.github.io/Liga-Comercial-Rally-Rodrigo-Rico/liga_comercial_rally.html) | Prototipo navegable de la app (Nivel 2): dashboard, registro de puntos, ranking, zonas, seguimiento, premios y reglas. Click en el nombre para verlo en vivo, o abrilo en cualquier navegador. |
| [`rally_resumen_semanal.json`](rally_resumen_semanal.json) | Workflow de n8n listo para importar: disparador semanal → Google Sheets → cálculo de ranking/alertas → Claude (IA) → email al jefe de ventas. |
| [`proceso_antes.png`](proceso_antes.png) / [`proceso_despues.png`](proceso_despues.png) | Diagramas del proceso **antes** y **después**. |
| [`prompts_del_proyecto.md`](prompts_del_proyecto.md) | Prompts diseñados: el que usa el workflow en producción y los usados durante el desarrollo (metodología). |
| [`Liga_Comercial_TP_Final_Rodrigo_Rico.pdf`](Liga_Comercial_TP_Final_Rodrigo_Rico.pdf) | Informe final del TP con el análisis completo (a–f) y evaluación AIBPS. |

## Cómo usarlo

1. **Ver la maqueta:** [abrila en vivo acá](https://rodrigoricodata.github.io/Liga-Comercial-Rally-Rodrigo-Rico/liga_comercial_rally.html), o descargá `liga_comercial_rally.html` y abrila en el navegador (no requiere servidor).
2. **Importar el workflow:** en n8n → *Workflows → Import from File* → seleccionar `rally_resumen_semanal.json`.
3. **Conectar credenciales:** cuenta de Google Sheets (hoja `puntos` con columnas `fecha, vendedor, zona, punto, canal, monto_bs, estado, validado, dias_sin_recompra`), API key de Anthropic y SMTP/Gmail para el envío.
4. **Reemplazar los placeholders** marcados como `REEMPLAZAR_...` en el JSON (ID del Sheet, email del jefe de ventas, URL del dashboard).

## El proceso, en una línea

**Antes:** rally informal → autoreporte por WhatsApp → Excel de dos columnas → premio a ciegas.
**Después:** registro validado en campo → datos centralizados → ranking automático → IA que alerta → jefe de ventas que decide.

## Herramientas

- **n8n** — orquestación del flujo automatizado (disparador, datos, email).
- **Claude (Anthropic API)** — redacción del resumen ejecutivo semanal y alertas comerciales. *La IA sugiere; el jefe de ventas decide.*
- **Google Sheets** — base de datos simple y auditable de los puntos abiertos.
- **HTML/CSS/JS** — maqueta navegable de la experiencia del vendedor y del ranking.

## Estado del proyecto

Nivel 2 (prototipo navegable + workflow diseñado y exportado). El diseño está listo para escalar a Nivel 1 conectando las credenciales reales — el análisis crítico y los siguientes pasos están en el informe PDF que acompaña este repositorio.

---
*Autor: Rodrigo Alejandro Rico Urquizu · 86RI43856@campus.economicas.uba.ar*
