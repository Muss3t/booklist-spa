<!-- 
======================================================================
Lección 2: Templates y rendering
Objetivo: Utilizar templates y directivas para representar datos.

Tareas a desarrollar:
Crear un componente Libro.vue para mostrar datos de un libro usando v-bind.
Usar v-if, v-show y v-for para mostrar/ocultar elementos o iterar sobre la lista de libros.
Mostrar un mensaje si no hay libros disponibles.
======================================================================
-->
<script setup>
import { defineProps } from 'vue'

// Definimos los props: Este componente ESPERA recibir un objeto llamado "libro"
const props = defineProps({
  libro: {
    type: Object,
    required: true
  }
})
</script>

<template>
  <div class="libro-card">
    <!-- Usamos {{ }} para renderizar los datos del objeto libro -->
    <h3>{{ libro.titulo }}</h3>
    <p><strong>Autor:</strong> {{ libro.autor }}</p>
    <p><strong>Categoría:</strong> {{ libro.categoria }}</p>
    
    <!-- Directiva v-show: La etiqueta siempre existe en el HTML, 
         pero solo se hace visible si la categoría es Ficción -->
    <span v-show="libro.categoria === 'Ficción'" class="badge">🔥 Ficción</span>
  </div>
</template>

<style scoped>
/* El modificador "scoped" hace que estos estilos solo afecten a este componente */
.libro-card {
  border: 1px solid #ddd;
  padding: 15px;
  border-radius: 8px;
  margin-bottom: 10px;
  background-color: #fff;
  text-align: left;
  box-shadow: 0 2px 4px rgba(0,0,0,0.05);
}
.badge {
  display: inline-block;
  background-color: #ff9800;
  color: white;
  padding: 3px 8px;
  border-radius: 12px;
  font-size: 12px;
  margin-top: 5px;
}
</style>