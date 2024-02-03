<template>
  <div id="app">
    <header class="navbar navbar-dark bg-custom">
      <div class="container">
        <span class="navbar-brand">Juego de Memoria</span>
      </div>
    </header>

    <main>
      <JuegoMemoria />
    </main>
  </div>
</template>

<script>
import JuegoMemoria from './components/JuegoMemoria.vue';

export default {
  components: {
    JuegoMemoria,
  },
};
</script>

<style>
body {
  margin: 0;
  padding: 0;
  font-family: 'Arial', sans-serif;
  background-image: url('./assets/back2.png');
  background-repeat: repeat;
}

header {
  background-color: #3a1c3d; /* El color especificado con opacidad (75) */
  /* Otras propiedades de estilo para el header */
}

main {
  margin-top: 20px;
}
</style>
