<!-- 
======================================================================
Lección 1: Introducción a Vue.js
Objetivo: Comprender la estructura básica de un componente Vue.
Tareas: App.vue, contador básico y patrón MVVM.
======================================================================
-->
<script setup>
import { ref } from 'vue'
// 1. IMPORTAMOS EL COMPONENTE HIJO
import Libro from './components/Libro.vue' 

// --- VARIABLES LECCIÓN 1 ---
const nombreUsuario = ref('Kisi') 
const contador = ref(0)
const incrementar = () => { contador.value++ }
const disminuir = () => { if (contador.value > 0) contador.value-- }

// --- VARIABLES LECCIÓN 2 ---
// 2. Creamos una lista reactiva simulando una base de datos de libros
const libros = ref([
  { id: 1, titulo: 'El principito', autor: 'Antoine de Saint-Exupéry', categoria: 'Ficción' },
  { id: 2, titulo: 'Hábitos Atómicos', autor: 'James Clear', categoria: 'Autoayuda' },
  { id: 3, titulo: '1984', autor: 'George Orwell', categoria: 'Ficción' }
])
</script>

<template>
  <div class="app-container">
    <header>
      <h1>Editorial Nova - BookList SPA</h1>
      <p>Bienvenido/a al sistema, <strong>{{ nombreUsuario }}</strong></p>
    </header>

    <!-- BLOQUE LECCIÓN 1 -->
    <main class="lesson-one">
      <h2>Lección 1: Contador Básico</h2>
      <div class="counter-box">
        <p>Libros registrados en esta sesión: <span>{{ contador }}</span></p>
        <div class="buttons">
          <button @click="disminuir" :disabled="contador === 0">- Quitar</button>
          <button @click="incrementar">+ Añadir</button>
        </div>
      </div>
    </main>

    <hr class="divisor" />

    <!-- BLOQUE LECCIÓN 2 -->
    <section class="lesson-two">
      <h2>Lección 2: Catálogo de Libros</h2>
      
      <!-- Directiva v-if: Se muestra SOLO si el arreglo está vacío -->
      <div v-if="libros.length === 0" class="mensaje-vacio">
        <p>No hay libros disponibles en este momento.</p>
      </div>

      <!-- Directiva v-else: Si hay libros, itera el componente <Libro> -->
      <div v-else class="lista-libros">
        <!-- Usamos v-for para iterar.
             Usamos :libro="libro" (v-bind) para inyectar la información al hijo -->
        <Libro 
          v-for="libro in libros" 
          :key="libro.id" 
          :libro="libro" 
        />
      </div>
    </section>
  </div>
</template>

<style>
/* Estilos Globales */
.app-container { font-family: Arial, sans-serif; max-width: 800px; margin: 0 auto; padding: 20px; text-align: center; }
header { background-color: #2c3e50; color: white; padding: 20px; border-radius: 8px; margin-bottom: 30px; }

/* Estilos Lección 1 */
.counter-box { background-color: #f9f9f9; border: 1px solid #ddd; padding: 20px; border-radius: 8px; display: inline-block; }
.counter-box span { font-size: 24px; font-weight: bold; color: #42b983; }
.buttons { margin-top: 15px; display: flex; gap: 10px; justify-content: center; }
button { padding: 10px 15px; border: none; border-radius: 4px; background-color: #42b983; color: white; cursor: pointer; font-weight: bold; }
button:disabled { background-color: #ccc; cursor: not-allowed; }
button:hover:not(:disabled) { background-color: #33a06f; }

/* Estilos Lección 2 */
.divisor { margin: 40px 0; border: 0; border-top: 2px dashed #ccc; }
.lesson-two { background-color: #f0f7f4; padding: 20px; border-radius: 8px; }
.mensaje-vacio { padding: 20px; color: #d9534f; background-color: #fdf7f7; border: 1px solid #ebccd1; border-radius: 4px; }
.lista-libros { display: flex; flex-direction: column; gap: 10px; }
</style>