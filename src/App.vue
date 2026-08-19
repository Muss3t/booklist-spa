<!-- 
======================================================================
Lección 1: Introducción a Vue.js
Objetivo: Comprender la estructura básica de un componente Vue.
Tareas a desarrollar:
● Crear el componente principal App.vue con estructura template/script/style.
● Implementar un contador básico con datos reactivos (data, methods).
● Aplicar el patrón MVVM y mostrar el nombre del usuario.

======================================================================
Lección 2: Templates y rendering
Objetivo: Utilizar templates y directivas para representar datos.
Tareas a desarrollar:
● Crear un componente Libro.vue para mostrar datos de un libro usando v-bind.
● Usar v-if, v-show y v-for para mostrar/ocultar elementos o iterar sobre la lista de libros.
● Mostrar un mensaje si no hay libros disponibles.

======================================================================
Lección 3: Binding de formularios
Objetivo: Implementar formularios interactivos con v-model.
Tareas a desarrollar:
● Crear un formulario que permita añadir libros con input, select y textarea.
● Utilizar v-model para vincular campos al modelo.
● Mostrar en tiempo real los datos ingresados.
======================================================================
-->

<script setup>
import { ref } from 'vue'
import Libro from './components/Libro.vue' 

// --- VARIABLES LECCIÓN 1 ---
const nombreUsuario = ref('Kisi') 
const contador = ref(0)
const incrementar = () => { contador.value++ }
const disminuir = () => { if (contador.value > 0) contador.value-- }

// --- VARIABLES LECCIÓN 2 ---
const libros = ref([
  { id: 1, titulo: 'El principito', autor: 'Antoine de Saint-Exupéry', categoria: 'Ficción' },
  { id: 2, titulo: 'Hábitos Atómicos', autor: 'James Clear', categoria: 'Autoayuda' },
  { id: 3, titulo: '1984', autor: 'George Orwell', categoria: 'Ficción' }
])

// --- VARIABLES LECCIÓN 3 ---
// Creamos un objeto reactivo para almacenar temporalmente lo que el usuario escribe
const nuevoLibro = ref({
  titulo: '',
  autor: '',
  categoria: '',
  descripcion: ''
})
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

    <!-- BLOQUE LECCIÓN 3 (arriba para que sea fácil ingresar datos) -->
    <section class="lesson-three">
      <h2>Lección 3: Registrar Nuevo Libro</h2>
      
      <div class="form-grid">
        <!-- Formulario -->
        <form class="formulario">
          <div class="form-group">
            <label>Título del libro:</label>
            <!-- v-model conecta este input con nuevoLibro.titulo -->
            <input type="text" v-model="nuevoLibro.titulo" placeholder="Ej. El Hobbit" />
          </div>

          <div class="form-group">
            <label>Autor:</label>
            <input type="text" v-model="nuevoLibro.autor" placeholder="Ej. J.R.R. Tolkien" />
          </div>

          <div class="form-group">
            <label>Categoría (Select):</label>
            <select v-model="nuevoLibro.categoria">
              <option disabled value="">Seleccione una categoría...</option>
              <option value="Ficción">Ficción</option>
              <option value="Autoayuda">Autoayuda</option>
              <option value="Educación">Educación</option>
              <option value="Tecnología">Tecnología</option>
            </select>
          </div>

          <div class="form-group">
            <label>Descripción corta (Textarea):</label>
            <textarea v-model="nuevoLibro.descripcion" placeholder="Escribe un breve resumen..."></textarea>
          </div>
        </form>

        <!-- Vista Previa en Tiempo Real -->
        <div class="preview-box">
          <h3>Vista Previa en Tiempo Real</h3>
          <p><strong>Título:</strong> <span class="highlight">{{ nuevoLibro.titulo || '---' }}</span></p>
          <p><strong>Autor:</strong> <span class="highlight">{{ nuevoLibro.autor || '---' }}</span></p>
          <p><strong>Categoría:</strong> <span class="highlight">{{ nuevoLibro.categoria || '---' }}</span></p>
          <p><strong>Descripción:</strong> <span class="highlight">{{ nuevoLibro.descripcion || '---' }}</span></p>
        </div>
      </div>
    </section>

    <hr class="divisor" />

    <!-- BLOQUE LECCIÓN 2 -->
    <section class="lesson-two">
      <h2>Lección 2: Catálogo de Libros</h2>
      <div v-if="libros.length === 0" class="mensaje-vacio">
        <p>No hay libros disponibles en este momento.</p>
      </div>
      <div v-else class="lista-libros">
        <Libro v-for="libro in libros" :key="libro.id" :libro="libro" />
      </div>
    </section>
  </div>
</template>

<style>
/* Estilos Globales, Lección 1 y 2 */
.app-container { font-family: Arial, sans-serif; max-width: 900px; margin: 0 auto; padding: 20px; text-align: center; }
header { background-color: #2c3e50; color: white; padding: 20px; border-radius: 8px; margin-bottom: 30px; }
.counter-box { background-color: #f9f9f9; border: 1px solid #ddd; padding: 20px; border-radius: 8px; display: inline-block; }
.counter-box span { font-size: 24px; font-weight: bold; color: #42b983; }
.buttons { margin-top: 15px; display: flex; gap: 10px; justify-content: center; }
button { padding: 10px 15px; border: none; border-radius: 4px; background-color: #42b983; color: white; cursor: pointer; font-weight: bold; }
button:disabled { background-color: #ccc; cursor: not-allowed; }
button:hover:not(:disabled) { background-color: #33a06f; }
.divisor { margin: 40px 0; border: 0; border-top: 2px dashed #ccc; }
.lesson-two { background-color: #f0f7f4; padding: 20px; border-radius: 8px; }
.mensaje-vacio { padding: 20px; color: #d9534f; background-color: #fdf7f7; border: 1px solid #ebccd1; border-radius: 4px; }
.lista-libros { display: flex; flex-direction: column; gap: 10px; }

/* Nuevos Estilos Lección 3 */
.lesson-three { background-color: #fdfbf7; padding: 20px; border-radius: 8px; border: 1px solid #f0e6d2; }
.form-grid { display: flex; gap: 20px; text-align: left; margin-top: 20px; flex-wrap: wrap; }
.formulario { flex: 1; background: white; padding: 20px; border-radius: 8px; box-shadow: 0 2px 5px rgba(0,0,0,0.05); min-width: 300px; }
.form-group { margin-bottom: 15px; }
.form-group label { display: block; font-weight: bold; margin-bottom: 5px; color: #333; }
.form-group input, .form-group select, .form-group textarea { width: 100%; padding: 10px; border: 1px solid #ccc; border-radius: 4px; font-family: inherit; box-sizing: border-box; }
.form-group textarea { resize: vertical; min-height: 80px; }
.preview-box { flex: 1; background-color: #2c3e50; color: white; padding: 20px; border-radius: 8px; min-width: 300px; }
.preview-box h3 { color: #42b983; margin-top: 0; }
.highlight { color: #f39c12; font-weight: bold; }
</style>