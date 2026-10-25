## Auditoría del Código

* **Selector universal inválido en CSS:** 
  Al inicio de tu archivo CSS tienes escrito `- { box-sizing: border-box; }`. El guion `-` es un error tipográfico y debe ser un asterisco (`*`).

* **Atributo `aria-describedby` malformado en HTML:** 
  En el campo de carga de archivo, colocaste el texto descriptivo completo directamente dentro del atributo en lugar de apuntar únicamente al ID del elemento de ayuda (`aria-describedby="ayuda-archivo"`).

* **Comentario mal ubicado dentro de una regla CSS:** 
  Dentro de las llaves del selector `header`, hay un comentario pegado a una propiedad (`flex-wrap: wrap;/* Formularios */`). Los comentarios deben ir siempre fuera de los bloques de declaraciones de estilo.