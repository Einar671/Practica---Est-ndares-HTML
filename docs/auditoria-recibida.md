# Auditoría a Biblioteca Barrial (Ficha N.º 13)

Biblioteca barrial · campo de carga de archivo con tipos restringidos · breakpoint 900 px · menú de navegación sin clases ni IDs (solo selectores estructurales y de atributo).

## 1. Qué esperaba y qué encontré

| Requisito | Esperaba | Encontré | Resultado |
|---|---|---|---|
| Biblioteca Barrial | Contenido de catálogo de libros, secciones de préstamo y formulario | Catálogo, sección de socios y formulario con carga de archivos | Cumple |
| Carga de archivo con tipos restringidos | `input type="file"` con atributo `accept`, `label` y ayuda accesible | Existe el campo de carga, pero el atributo `aria-describedby` está malformado | Parcial |
| Breakpoint 900 px | `@media (min-width: 900px)` que adapte el diseño principal | Definido correctamente en el archivo CSS | Cumple |
| Menú sin clases ni IDs | Uso exclusivo de selectores estructurales (`nav ul li`) y de atributo | El menú de navegación cumple estrictamente sin usar clases ni IDs | Cumple |

Validador W3C (Nu): HTML y CSS con errores de sintaxis (selector universal inválido).

## 2. Informe de auditoría

| N.º | Requisito | Ubicación | Hallazgo | Norma que incumple | Evidencia | Severidad |
|---|---|---|---|---|---|---|
| 1 | Sintaxis y validadores CSS | `estilos.css`, línea 1 | Al inicio del archivo CSS se encuentra escrito `- { box-sizing: border-box; }`. El guion `-` es un error tipográfico y debe ser un asterisco (`*`). | W3C CSS Validation (Sintaxis de selectores) | Captura del archivo CSS con el selector inválido | Alta |
| 2 | Campo de carga de archivo (Accesibilidad) | `index.html`, campo de carga de archivo | En el campo de carga de archivo, se colocó el texto descriptivo completo directamente dentro del atributo en lugar de apuntar únicamente al ID del elemento de ayuda (`aria-describedby="ayuda-archivo"`). | WCAG 2.2, criterio 4.1.2 (Nombre, función, valor) | Captura del HTML con la descripción directa en el atributo | Media |
| 3 | Estructura y formato CSS | `estilos.css`, selector `header` | Dentro de las llaves del selector `header`, hay un comentario pegado directamente a una propiedad (`flex-wrap: wrap;/* Formularios */`). Los comentarios deben ir fuera de los bloques de declaraciones. | W3C CSS / Buenas prácticas de formato | Captura del bloque CSS con el comentario interno | Baja |