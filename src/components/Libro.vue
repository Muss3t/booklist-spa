<!-- 
======================================================================
Lección 2 y 4: Componente Libro con Emisión de Eventos
======================================================================
-->
<script setup>
import { defineProps, defineEmits } from 'vue'

const props = defineProps({
  libro: {
    type: Object,
    required: true
  }
})

// Definimos el evento personalizado que este componente emitirá hacia App.vue
const emit = defineEmits(['eliminar'])
</script>

<template>
  <div class="libro-card">
    <div class="info-texto">
      <h3>{{ libro.titulo }}</h3>
      <p><strong>Autor:</strong> {{ libro.autor }}</p>
      <p><strong>Categoría:</strong> {{ libro.categoria }}</p>
      <span v-show="libro.categoria === 'Ficción'" class="badge">🔥 Ficción</span>
    </div>
    
    <!-- @click simple para emitir el evento 'eliminar' pasándole el ID del libro -->
    <button class="btn-eliminar" @click="emit('eliminar', libro.id)">🗑️ Eliminar</button>
  </div>
</template>

<style scoped>
.libro-card {
  border: 1px solid #ddd;
  padding: 15px;
  border-radius: 8px;
  margin-bottom: 10px;
  background-color: #fff;
  text-align: left;
  box-shadow: 0 2px 4px rgba(0,0,0,0.05);
  /* Flexbox para alinear el texto a la izquierda y el botón a la derecha */
  display: flex;
  justify-content: space-between; 
  align-items: center;
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
.btn-eliminar {
  background-color: #ff4d4d;
  color: white;
  border: none;
  padding: 10px 15px;
  border-radius: 6px;
  cursor: pointer;
  font-weight: bold;
}
.btn-eliminar:hover {
  background-color: #cc0000;
}
</style>