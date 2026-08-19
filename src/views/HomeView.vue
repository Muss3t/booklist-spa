<script setup>
import { ref } from 'vue'
// IMPORTANTE: Actualizamos la ruta
import Libro from '../components/Libro.vue' 

const nombreUsuario = ref('Kisi') 
const contador = ref(0)
const incrementar = () => { contador.value++ }
const disminuir = () => { if (contador.value > 0) contador.value-- }

const libros = ref([
  { id: 1, titulo: 'El principito', autor: 'Antoine de Saint-Exupéry', categoria: 'Ficción' },
  { id: 2, titulo: 'Hábitos Atómicos', autor: 'James Clear', categoria: 'Autoayuda' }
])

const nuevoLibro = ref({ titulo: '', autor: '', categoria: '', descripcion: '' })

const agregarLibro = () => {
  if (nuevoLibro.value.titulo.trim() === '') {
    alert('Por favor, ingresa al menos el título.')
    return
  }
  libros.value.push({
    id: Date.now(),
    titulo: nuevoLibro.value.titulo,
    autor: nuevoLibro.value.autor || 'Desconocido',
    categoria: nuevoLibro.value.categoria || 'Sin categoría'
  })
  nuevoLibro.value = { titulo: '', autor: '', categoria: '', descripcion: '' }
}

const eliminarLibro = (idLibro) => {
  libros.value = libros.value.filter(libro => libro.id !== idLibro)
}

const mostrarTip = () => {
  alert('¡Tip! Puedes guardar más rápido presionando la tecla Enter dentro de las cajas de texto.')
}
</script>

<template>
  <div class="home-container">
    <header class="header-principal">
      <h1>Editorial Nova - BookList SPA</h1>
      <p>Bienvenido/a al sistema, <strong>{{ nombreUsuario }}</strong></p>
      <button class="btn-tip" @click.once="mostrarTip">Ver Tip de Uso (1 vez)</button>
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

    <hr class="divisor" />

    <section class="lesson-three">
      <h2>Lecciones 3 y 4: Registrar Nuevo Libro</h2>
      <div class="form-grid">
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
          <button type="submit" class="btn-guardar">Guardar Libro</button>
        </form>

        <div class="preview-box">
          <h3>Vista Previa en Tiempo Real</h3>
          <p><strong>Título:</strong> <span class="highlight">{{ nuevoLibro.titulo || '---' }}</span></p>
          <p><strong>Autor:</strong> <span class="highlight">{{ nuevoLibro.autor || '---' }}</span></p>
          <p><strong>Categoría:</strong> <span class="highlight">{{ nuevoLibro.categoria || '---' }}</span></p>
        </div>
      </div>
    </section>

    <hr class="divisor" />

    <section class="lesson-two">
      <h2>Lección 2 y 4: Catálogo de Libros</h2>
      <div v-if="libros.length === 0" class="mensaje-vacio">
        <p>No hay libros disponibles en este momento.</p>
      </div>
      <div v-else class="lista-libros">
        <Libro v-for="libro in libros" :key="libro.id" :libro="libro" @eliminar="eliminarLibro" />
      </div>
    </section>
  </div>
</template>