<!-- 
======================================================================
Lección 1: Componente, MVVM y estado (Hecho)
Lección 2: Templates, v-for, v-show (Hecho)
Lección 3: Binding de formularios v-model (Hecho)
Lección 4: Manejo de eventos (Hecho)
Lección 5: Enrutamiento con Vue Router (hecho)
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
      <RouterLink to="/" class="nav-link"> Inicio (Gestor)</RouterLink>
      <RouterLink to="/about" class="nav-link">Acerca de</RouterLink>
    </nav>

    <!-- HomeView.vue o AboutView.vue -->
    <RouterView />
  </div>
</template>

<style>
/* --- VARIABLES DE DISEÑO MODERNO --- */
:root {
  --primary: #3b82f6;
  --primary-hover: #2563eb;
  --bg-color: #f8fafc;
  --card-bg: #ffffff;
  --text-main: #1e293b;
  --text-muted: #64748b;
  --border-color: #e2e8f0;
}

body {
  background-color: var(--bg-color);
  color: var(--text-main);
  margin: 0;
  padding: 0;
}

.app-wrapper { font-family: 'Segoe UI', system-ui, -apple-system, sans-serif; max-width: 960px; margin: 0 auto; padding: 20px; }

/* NAVBAR ELEGANTE */
.navbar { display: flex; justify-content: center; gap: 15px; background-color: var(--card-bg); padding: 15px; border-radius: 16px; margin-bottom: 30px; box-shadow: 0 4px 6px -1px rgba(0,0,0,0.05); border: 1px solid var(--border-color); }
.nav-link { color: var(--text-muted); text-decoration: none; font-weight: 600; padding: 10px 24px; border-radius: 10px; transition: all 0.2s ease; }
.nav-link:hover { background-color: #f1f5f9; color: var(--text-main); }
.router-link-exact-active { background-color: var(--primary); color: white !important; box-shadow: 0 2px 4px rgba(59,130,246,0.3); }
.router-link-exact-active:hover { background-color: var(--primary-hover); }

/* HEADER PRINCIPAL */
.header-principal { background: linear-gradient(135deg, #1e293b, #334155); color: white; padding: 35px 20px; border-radius: 20px; margin-bottom: 40px; text-align: center; box-shadow: 0 10px 15px -3px rgba(0,0,0,0.1); }
.header-principal h1 { margin: 0 0 10px 0; font-size: 32px; letter-spacing: -0.5px; }
.btn-tip { background-color: rgba(255,255,255,0.15); color: white; border: 1px solid rgba(255,255,255,0.2); padding: 8px 18px; border-radius: 20px; cursor: pointer; margin-top: 15px; font-weight: 600; transition: all 0.2s; backdrop-filter: blur(5px); }
.btn-tip:hover { background-color: rgba(255,255,255,0.25); transform: translateY(-1px); }

/* CONTENEDORES Y TIPOGRAFÍA */
h2 { color: var(--text-main); font-size: 24px; margin-bottom: 25px; letter-spacing: -0.5px; border-bottom: 2px solid var(--border-color); padding-bottom: 10px; display: inline-block;}
.divisor { margin: 50px 0; border: 0; border-top: 1px solid var(--border-color); }
.counter-box { background-color: var(--card-bg); border: 1px solid var(--border-color); padding: 30px; border-radius: 16px; display: inline-block; text-align: center; box-shadow: 0 4px 6px -1px rgba(0,0,0,0.03); min-width: 300px; }
.counter-box p { margin: 0 0 15px 0; color: var(--text-muted); font-size: 16px;}
.counter-box span { font-size: 36px; font-weight: 800; color: var(--primary); display: block; margin-bottom: 20px;}

/* BOTONES GENERALES */
.buttons { display: flex; gap: 12px; justify-content: center; }
button { padding: 12px 24px; border: none; border-radius: 10px; background-color: var(--primary); color: white; cursor: pointer; font-weight: 600; transition: all 0.2s; font-size: 15px;}
button:disabled { background-color: #cbd5e1; cursor: not-allowed; }
button:hover:not(:disabled) { background-color: var(--primary-hover); transform: translateY(-2px); box-shadow: 0 4px 6px rgba(59,130,246,0.2); }

/* FORMULARIO */
.form-grid { display: flex; gap: 30px; text-align: left; align-items: stretch; flex-wrap: wrap; }
.formulario { flex: 1.2; background: var(--card-bg); padding: 30px; border-radius: 16px; box-shadow: 0 4px 6px -1px rgba(0,0,0,0.03); border: 1px solid var(--border-color); min-width: 320px; }
.form-group { margin-bottom: 20px; }
.form-group label { display: block; font-weight: 600; margin-bottom: 8px; color: var(--text-main); font-size: 14px; }
.form-group input, .form-group select, .form-group textarea { width: 100%; padding: 12px 15px; border: 1px solid var(--border-color); border-radius: 10px; font-family: inherit; font-size: 15px; box-sizing: border-box; transition: all 0.2s; background-color: #f8fafc; color: var(--text-main);}
.form-group input:focus, .form-group select:focus, .form-group textarea:focus { outline: none; border-color: var(--primary); background-color: white; box-shadow: 0 0 0 4px rgba(59,130,246,0.1); }
.form-group textarea { resize: vertical; min-height: 120px; }
.btn-guardar { width: 100%; font-size: 16px; padding: 14px; margin-top: 10px; }

/* VISTA PREVIA OSCURA */
.preview-box { flex: 1; background: linear-gradient(135deg, #0f172a, #1e293b); color: white; padding: 30px; border-radius: 16px; min-width: 300px; box-shadow: 0 10px 15px -3px rgba(0,0,0,0.1); }
.preview-box h3 { color: #38bdf8; margin-top: 0; margin-bottom: 25px; border-bottom: 1px solid rgba(255,255,255,0.1); padding-bottom: 15px; font-size: 18px;}
.preview-box p { margin-bottom: 15px; color: #94a3b8; font-size: 15px;}
.highlight { color: #f8fafc; font-weight: 600; font-size: 18px; display: block; margin-top: 6px; }

/* CATÁLOGO Y MENSAJES */
.mensaje-vacio { padding: 30px; color: #b45309; background-color: #fffbeb; border: 1px solid #fde68a; border-radius: 16px; text-align: center; font-weight: 600; font-size: 16px;}
.lista-libros { display: flex; flex-direction: column; gap: 15px; }
</style>