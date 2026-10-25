# Respuesta a la auditoría recibida

| N.º de hallazgo | Decisión | Justificación con la norma | Evidencia antes y después | Commit |
|---|---|---|---|---|
| 1. Selector `-` en vez de `*` | **Refuta** | `css/estilos.css`, línea 10: `* { box-sizing: border-box; }` es un selector universal válido (Selectors Level 4, §5.1). No existe ninguna regla `- { }` en el archivo (`grep -nE '^\s*-\s*\{'` sin resultados). | Antes y después: sin cambio. Validador Nu: CSS con 0 errores (`docs/evidencia/validador-antes.txt`). | Ninguno |
| 2. `aria-describedby` malformado | **Acepta, con corrección de ubicación** | El `<input type="file">` (línea 40) está bien: `aria-describedby="ayuda-archivo"` apunta a un ID existente. El error real está en el `<p id="ayuda-archivo">` (línea 41), que tenía `aria-describedby` con texto literal. ARIA 1.2 exige una lista de IDs; ese valor no apunta a ningún elemento. Es innecesario porque el `<p>` ya contiene el texto. WCAG 4.1.2. Severidad: baja. | Antes: `<p id="ayuda-archivo" aria-describedby="Formatos permitidos…">`. Después: `<p id="ayuda-archivo">`. El validador Nu no lo detecta en ninguno de los dos casos. | `Decimo Commit` |
| 3. Comentario dentro de la regla `header` | **Acepta como legibilidad, refuta la norma** | `flex-wrap: wrap;/* Formularios */` (línea 57) es CSS válido: CSS Syntax Level 3 permite comentarios en cualquier lugar. La afirmación de que "deben ir siempre fuera" es falsa. Sí es un defecto real: el comentario "Formularios" aparece dentro de `header` y confunde, porque esa sección está en la línea 107. | Antes: `flex-wrap: wrap;/* Formularios */`. Después: `flex-wrap: wrap;`. Nu: 0 errores antes y después. | `Decimo Commit` |

## Problemas que el auditor no detectó

| N.º | Hallazgo | Norma | Evidencia antes y después | Commit |
|---|---|---|---|---|
| A | El CSS define `body > a:first-child` ("Saltar al contenido", líneas 39-50) pero el HTML no tiene ese enlace; las reglas nunca se aplican. Se agrega `<a href="#principal">Saltar al contenido</a>` como primer hijo de `body` (el `id="principal"` ya existía en `main`). | WCAG 2.2, criterio 2.4.1 Evitar bloques | Antes: Tab primero enfoca el logo; el selector no coincide con ningún elemento. Después: Tab primero muestra el enlace, que lleva a `main`.| `Decimo commit` |
| B | La tabla de horarios tiene 7 columnas y no cabe en 320 px: la página se desplaza en horizontal. Se envuelve en `<div role="region" aria-label="Horarios" tabindex="0">` con `overflow-x: auto`, sin cambiar el `display` de la tabla. | WCAG 2.2, criterios 1.4.10 Reflow y 2.1.1 Teclado | Antes: desplazamiento horizontal de toda la página a 320 px. Después: solo se desplaza la tabla y es alcanzable con Tab.| `Decimo commit` |

## Validación final

Nu Html Checker (W3C) sobre `index.html` y `css/estilos.css`: 0 errores y 0 advertencias antes y después (`docs/evidencia/validador-antes.txt` y `validador-despues.txt`).
