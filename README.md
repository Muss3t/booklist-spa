# Editorial Nova - BookList SPA

Una Single Page Application (SPA) desarrollada con Vue.js para la gestión del catálogo de libros de la Editorial Nova. Este proyecto corresponde a la entrega final del Módulo 6.

## Maqueta Funcional

Puedes revisar la versión funcional y el diseño de la interfaz en el siguiente enlace:
**[Haz clic aquí para ver la maqueta funcional](https://muss3t.github.io/booklist-spa/)**

## Tecnologías y Conceptos Aplicados

Este proyecto fue construido aplicando los requerimientos clave del módulo:

* **Arquitectura de Componentes:** Uso del patrón MVVM y separación entre componentes padre (`App.vue`) e hijo (`Libro.vue`).
* **Renderizado Declarativo:** Uso de directivas estructurales como `v-for`, `v-if` y `v-show` para iterar y condicionar la vista.
* **Reactividad Bidireccional:** Implementación de formularios interactivos utilizando `v-model`.
* **Manejo de Eventos:** Captura de acciones del usuario (`@click`, `@keyup.enter`), uso de modificadores (`.prevent`, `.once`) y emisión de eventos (`defineEmits`).
* **Enrutamiento (SPA):** Configuración de múltiples vistas (`HomeView.vue` y `AboutView.vue`) utilizando Vue Router sin recarga de página.


---
*Desarrollado por Kisi Toledo*