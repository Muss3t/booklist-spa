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
  border: 1px solid #e2e8f0;
  padding: 20px 25px;
  border-radius: 16px;
  background-color: #ffffff;
  text-align: left;
  display: flex;
  justify-content: space-between; 
  align-items: center;
  transition: all 0.2s ease;
  box-shadow: 0 2px 4px rgba(0,0,0,0.02);
}
.libro-card:hover {
  transform: translateY(-3px);
  box-shadow: 0 10px 15px -3px rgba(0,0,0,0.08);
  border-color: #cbd5e1;
}
.info-texto h3 { margin: 0 0 8px 0; color: #1e293b; font-size: 20px; }
.info-texto p { margin: 4px 0; color: #64748b; font-size: 15px; }
.badge {
  display: inline-block;
  background-color: #f59e0b;
  color: white;
  padding: 4px 12px;
  border-radius: 20px;
  font-size: 12px;
  font-weight: 700;
  margin-top: 10px;
  letter-spacing: 0.5px;
}
.btn-eliminar {
  background-color: #ef4444;
  color: white;
  border: none;
  padding: 10px 16px;
  border-radius: 10px;
  cursor: pointer;
  font-weight: 600;
  transition: all 0.2s;
}
.btn-eliminar:hover {
  background-color: #dc2828;
  transform: translateY(-2px);
  box-shadow: 0 4px 6px rgba(239, 68, 68, 0.2);
}
</style>