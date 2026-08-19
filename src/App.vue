<!-- 
======================================================================
Lección 1: Componente, MVVM y estado (Hecho)
Lección 2: Templates, v-for, v-show (Hecho)
Lección 3: Binding de formularios v-model (Hecho)

Lección 4: Manejo de eventos
Objetivo: Capturar eventos del usuario para modificar el estado.
Tareas a desarrollar:
● Usar @click para agregar y eliminar libros de la lista.
● Aplicar modificadores como .prevent y .once donde sea pertinente.
● Agregar eventos de teclado para agregar libros con Enter.npm
======================================================================
-->
<script setup>
import { ref } from 'vue'
import Libro from './components/Libro.vue' 

// --- LECCIÓN 1 ---
const nombreUsuario = ref('Kisi') 
const contador = ref(0)
const incrementar = () => { contador.value++ }
const disminuir = () => { if (contador.value > 0) contador.value-- }

// --- LECCIÓN 2 y 4 (Datos) ---
const libros = ref([
  { id: 1, titulo: 'El principito', autor: 'Antoine de Saint-Exupéry', categoria: 'Ficción' },
  { id: 2, titulo: 'Hábitos Atómicos', autor: 'James Clear', categoria: 'Autoayuda' }
])

// --- LECCIÓN 3 (Modelo del Formulario) ---
const nuevoLibro = ref({ titulo: '', autor: '', categoria: '', descripcion: '' })

// --- LÓGICA LECCIÓN 4 (Funciones y Eventos) ---

// 1. Agregar un libro nuevo
const agregarLibro = () => {
  if (nuevoLibro.value.titulo.trim() === '') {
    alert('Por favor, ingresa al menos el título.')
    return
  }

  // Agregamos al arreglo (Creamos un ID único usando Date.now)
  libros.value.push({
    id: Date.now(),
    titulo: nuevoLibro.value.titulo,
    autor: nuevoLibro.value.autor || 'Desconocido',
    categoria: nuevoLibro.value.categoria || 'Sin categoría'
  })

  // Limpiamos el formulario para el siguiente
  nuevoLibro.value = { titulo: '', autor: '', categoria: '', descripcion: '' }
}

// 2. Eliminar un libro recibiendo el ID desde el Hijo
const eliminarLibro = (idLibro) => {
  libros.value = libros.value.filter(libro => libro.id !== idLibro)
}

// 3. Modificador .once (Un tip que solo aparece 1 vez)
const mostrarTip = () => {
  alert('¡Tip! Puedes guardar más rápido presionando la tecla Enter dentro de las cajas de texto.')
}
</script>

<template>
  <div class="app-container">
    <header>
      <h1>📚 Editorial Nova - BookList SPA</h1>
      <p>Bienvenido/a al sistema, <strong>{{ nombreUsuario }}</strong></p>
      <!-- @click.once: Este botón solo funciona la primera vez que se toca -->
      <button class="btn-tip" @click.once="mostrarTip">💡 Ver Tip de Uso (1 vez)</button>
    </header>

    <!-- LECCIÓN 1 -->
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

    <!-- LECCIÓN 3 y 4 -->
    <section class="lesson-three">
      <h2>Lecciones 3 y 4: Registrar Nuevo Libro</h2>
      <div class="form-grid">
        
        <!-- @submit.prevent: Evita que la página recargue -->
        <!-- @keyup.enter: Si presionas Enter mientras estás en el form, ejecuta agregarLibro -->
        <form class="formulario" @submit.prevent="agregarLibro" @keyup.enter="agregarLibro">
          <div class="form-group">
            <label>Título del libro:</label>
            <input type="text" v-model="nuevoLibro.titulo" placeholder="Ej. El Hobbit" />
          </div>

          <div class="form-group">
            <label>Autor:</label>
            <input type="text" v-model="nuevoLibro.autor" placeholder="Ej. J.R.R. Tolkien" />
          </div>

          <div class="form-group">
            <label>Categoría:</label>
            <select v-model="nuevoLibro.categoria">
              <option disabled value="">Seleccione una categoría...</option>
              <option value="Ficción">Ficción</option>
              <option value="Autoayuda">Autoayuda</option>
              <option value="Educación">Educación</option>
              <option value="Tecnología">Tecnología</option>
            </select>
          </div>

          <div class="form-group">
            <label>Descripción corta:</label>
            <textarea v-model="nuevoLibro.descripcion" placeholder="Escribe un breve resumen..."></textarea>
          </div>

          <button type="submit" class="btn-guardar">💾 Guardar Libro</button>
        </form>

        <!-- Vista Previa -->
        <div class="preview-box">
          <h3>👁️ Vista Previa en Tiempo Real</h3>
          <p><strong>Título:</strong> <span class="highlight">{{ nuevoLibro.titulo || '---' }}</span></p>
          <p><strong>Autor:</strong> <span class="highlight">{{ nuevoLibro.autor || '---' }}</span></p>
          <p><strong>Categoría:</strong> <span class="highlight">{{ nuevoLibro.categoria || '---' }}</span></p>
        </div>
      </div>
    </section>

    <hr class="divisor" />

    <!-- LECCIÓN 2 y 4 -->
    <section class="lesson-two">
      <h2>Lección 2 y 4: Catálogo de Libros</h2>
      <div v-if="libros.length === 0" class="mensaje-vacio">
        <p>⚠️ No hay libros disponibles en este momento.</p>
      </div>
      <div v-else class="lista-libros">
        <!-- @eliminar="eliminarLibro" se queda escuchando al hijo -->
        <Libro 
          v-for="libro in libros" 
          :key="libro.id" 
          :libro="libro" 
          @eliminar="eliminarLibro" 
        />
      </div>
    </section>
  </div>
</template>

<style>
/* Estilos globales y anteriores */
.app-container { font-family: Arial, sans-serif; max-width: 900px; margin: 0 auto; padding: 20px; text-align: center; }
header { background-color: #2c3e50; color: white; padding: 20px; border-radius: 8px; margin-bottom: 30px; }
.btn-tip { background-color: #f39c12; color: white; border: none; padding: 8px 15px; border-radius: 20px; cursor: pointer; margin-top: 10px; font-weight: bold; }
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
.lesson-three { background-color: #fdfbf7; padding: 20px; border-radius: 8px; border: 1px solid #f0e6d2; }
.form-grid { display: flex; gap: 20px; text-align: left; margin-top: 20px; flex-wrap: wrap; }
.formulario { flex: 1; background: white; padding: 20px; border-radius: 8px; box-shadow: 0 2px 5px rgba(0,0,0,0.05); min-width: 300px; }
.form-group { margin-bottom: 15px; }
.form-group label { display: block; font-weight: bold; margin-bottom: 5px; color: #333; }
.form-group input, .form-group select, .form-group textarea { width: 100%; padding: 10px; border: 1px solid #ccc; border-radius: 4px; font-family: inherit; box-sizing: border-box; }
.preview-box { flex: 1; background-color: #2c3e50; color: white; padding: 20px; border-radius: 8px; min-width: 300px; }
.preview-box h3 { color: #42b983; margin-top: 0; }
.highlight { color: #f39c12; font-weight: bold; }
.btn-guardar { width: 100%; background-color: #007bff; font-size: 16px; padding: 12px; }
.btn-guardar:hover { background-color: #0056b3; }
</style>