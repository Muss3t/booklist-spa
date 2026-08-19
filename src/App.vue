<!-- 
======================================================================
Lección 1: Introducción a Vue.js
Objetivo: Comprender la estructura básica de un componente Vue.

Tareas a desarrollar:
Crear el componente principal App.vue con estructura template/script/style.
Implementar un contador básico con datos reactivos (data, methods).
Aplicar el patrón MVVM y mostrar el nombre del usuario.
======================================================================
-->
<script setup>
import { ref } from 'vue'

// 1. Patrón MVVM: Dato reactivo (Modelo) que se refleja en la Vista
const nombreUsuario = ref('Kisi') 

// 2. Dato reactivo para el contador
const contador = ref(0)

// 3. Lógica para modificar el estado (ViewModel)
const incrementar = () => {
  contador.value++
}

const disminuir = () => {
  if (contador.value > 0) {
    contador.value--
  }
}
</script>

<template>
  <div class="app-container">
    <header>
      <h1>📚 Editorial Nova - BookList SPA</h1>
      <p>Bienvenido/a al sistema, <strong>{{ nombreUsuario }}</strong></p>
    </header>

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
  </div>
</template>

<style>
.app-container {
  font-family: Arial, sans-serif;
  max-width: 800px;
  margin: 0 auto;
  padding: 20px;
  text-align: center;
}

header {
  background-color: #2c3e50;
  color: white;
  padding: 20px;
  border-radius: 8px;
  margin-bottom: 30px;
}

.counter-box {
  background-color: #f9f9f9;
  border: 1px solid #ddd;
  padding: 20px;
  border-radius: 8px;
  display: inline-block;
}

.counter-box span {
  font-size: 24px;
  font-weight: bold;
  color: #42b983;
}

.buttons {
  margin-top: 15px;
  display: flex;
  gap: 10px;
  justify-content: center;
}

button {
  padding: 10px 15px;
  border: none;
  border-radius: 4px;
  background-color: #42b983;
  color: white;
  cursor: pointer;
  font-weight: bold;
}

button:disabled {
  background-color: #ccc;
  cursor: not-allowed;
}

button:hover:not(:disabled) {
  background-color: #33a06f;
}
</style>