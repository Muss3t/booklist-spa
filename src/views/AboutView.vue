<template>
  <div class="about-container">
    <h2>Acerca de Editorial Nova</h2>
    <div class="about-card">
      <p>Este proyecto es el resultado final de las 5 lecciones de Vue.js.</p>
      <p><strong>Características:</strong></p>
      <ul>
        <li>Arquitectura de Componentes (Padre e Hijo)</li>
        <li>Directivas Estructurales (v-for, v-if, v-show)</li>
        <li>Reactividad Bidireccional (v-model)</li>
        <li>Emisión de Eventos Personalizados (emit)</li>
        <li>Enrutamiento (Vue Router)</li>
      </ul>
      <p>Desarrollado con éxito por <strong>Kisi</strong>.</p>
    </div>
  </div>
</template>

<style scoped>
.about-container { text-align: center; padding: 40px; }
.about-card { background: white; border: 1px solid #ddd; padding: 30px; border-radius: 8px; max-width: 600px; margin: 0 auto; box-shadow: 0 4px 8px rgba(0,0,0,0.1); text-align: left; }
.about-card ul { line-height: 1.8; }
</style>