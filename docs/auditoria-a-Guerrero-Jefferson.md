# Auditoría a Guerrero-Jefferson (Ficha N.º 12)

Agencia turística · campo `range` · breakpoint 900 px · modo oscuro con `prefers-color-scheme` sin duplicar reglas.

## 1. Qué esperaba y qué encontré

| Requisito | Esperaba | Encontré | Resultado |
|---|---|---|---|
| Agencia turística | Contenido de destinos, ofertas y reserva | Destinos, ofertas, tabla y formulario de reserva | Cumple |
| Campo `range` | `input type="range"` con `label`, `min`, `max` y valor visible | Existe con label (index.html:130); no muestra el valor | Parcial |
| Breakpoint 900 px | `@media (min-width: 900px)` que cambie el diseño y gane en la cascada | Existe (css:21-26) pero queda anulado | No cumple |
| Modo oscuro sin duplicar reglas | Un solo `@media (prefers-color-scheme: dark)` que redefina variables | Correcto (css:10-19); colores con poco contraste | Cumple la restricción; falla contraste |

Validador W3C (Nu): HTML y CSS sin errores.

## 2. Informe de auditoría

| N.º | Requisito | Ubicación | Hallazgo | Norma que incumple | Evidencia | Severidad |
|---|---|---|---|---|---|---|
| 1 | Breakpoint 900 px | css/estilos.css, líneas 21-26 y 81-87 | El `@media` tiene la misma especificidad (0,1,1) que `.destinos-grid article` y `.ofertas-grid article`, que van después y ganan. El breakpoint no cambia nada; con `flex-basis` de 300 px ya hay 2 columnas desde ~725 px | CSS Cascade Level 4, §6.1 (orden de aparición); requisito de la ficha | Captura: DevTools, Styles de `article` a 950 px, `flex` del media query tachado | Alta |
| 2 | Modo oscuro | css/estilos.css, líneas 14, 69-72, 130-133, 176-184 | Texto blanco sobre `#0a9396` (`th`, `button`, `nav a:hover`): contraste 3,73:1 | WCAG 2.2, criterio 1.4.3 (mín. 4,5:1) | Captura: DevTools con `prefers-color-scheme: dark`, selector de color del `th` con "3.73 ✖" | Media |
| 3 | Modo oscuro | css/estilos.css, líneas 17 y 155-163 | Borde de campos `#444` sobre `#1e1e1e`: 1,71:1 (también 1,53:1 en claro) | WCAG 2.2, criterio 1.4.11 (mín. 3:1) | Captura: DevTools, `border-color` de `input#nombre` en modo oscuro | Media |
| 4 | Campo `range` | index.html, línea 130 | No muestra el valor elegido (no hay `output`) | WCAG 2.2, criterio 3.3.2; HTML Living Standard, elemento `output` | Captura: slider movido a 7 sin número visible | Media |