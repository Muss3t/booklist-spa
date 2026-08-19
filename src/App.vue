<!-- 
======================================================================
Lección 1: Componente, MVVM y estado (Hecho)
Lección 2: Templates, v-for, v-show (Hecho)
Lección 3: Binding de formularios v-model (Hecho)
Lección 4: Manejo de eventos (Hecho)
Lección 5: Enrutamiento con Vue Router
Objetivo: Navegar entre distintas vistas de la aplicación.
Tareas a desarrollar:
● Configurar Vue Router con al menos dos rutas (Home y About).
● Usar <router-link> para la navegación.
● Usar <router-view> para renderizar los componentes de ruta.
======================================================================
-->
<script setup>
// Importamos las herramientas de enrutamiento
import { RouterLink, RouterView } from 'vue-router'
</script>

<template>
  <div class="app-wrapper">
    <!-- Barra de Navegación Global -->
    <nav class="navbar">
      <!-- RouterLink actúa como la etiqueta <a> pero sin recargar la página -->
      <RouterLink to="/" class="nav-link">🏠 Inicio (Gestor)</RouterLink>
      <RouterLink to="/about" class="nav-link">ℹ️ Acerca de</RouterLink>
    </nav>

    <!-- Aquí se inyectan dinámicamente el HomeView.vue o AboutView.vue -->
    <RouterView />
  </div>
</template>

<style>
/* Estilos del menú de navegación */
.app-wrapper { font-family: Arial, sans-serif; max-width: 900px; margin: 0 auto; padding: 20px; }
.navbar { display: flex; justify-content: center; gap: 20px; background-color: #2c3e50; padding: 15px; border-radius: 8px; margin-bottom: 30px; }
.nav-link { color: white; text-decoration: none; font-weight: bold; padding: 10px 20px; border-radius: 4px; transition: background-color 0.3s; }
.nav-link:hover { background-color: #33a06f; }

/* La clase .router-link-exact-active la añade Vue automáticamente a la página donde estás */
.router-link-exact-active { background-color: #42b983; }

/* --- ESTILOS GLOBALES DE TU APLICACIÓN --- */
.header-principal { background-color: #2c3e50; color: white; padding: 20px; border-radius: 8px; margin-bottom: 30px; text-align: center; }
.btn-tip { background-color: #f39c12; color: white; border: none; padding: 8px 15px; border-radius: 20px; cursor: pointer; margin-top: 10px; font-weight: bold; }
.counter-box { background-color: #f9f9f9; border: 1px solid #ddd; padding: 20px; border-radius: 8px; display: inline-block; text-align: center; }
.counter-box span { font-size: 24px; font-weight: bold; color: #42b983; }
.buttons { margin-top: 15px; display: flex; gap: 10px; justify-content: center; }
button { padding: 10px 15px; border: none; border-radius: 4px; background-color: #42b983; color: white; cursor: pointer; font-weight: bold; }
button:disabled { background-color: #ccc; cursor: not-allowed; }
button:hover:not(:disabled) { background-color: #33a06f; }
.divisor { margin: 40px 0; border: 0; border-top: 2px dashed #ccc; }
.lesson-two { background-color: #f0f7f4; padding: 20px; border-radius: 8px; }
.mensaje-vacio { padding: 20px; color: #d9534f; background-color: #fdf7f7; border: 1px solid #ebccd1; border-radius: 4px; text-align: center;}
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