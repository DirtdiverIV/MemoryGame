<template>
  <div id="app">
    <header class="navbar navbar-dark bg-primary">
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
}

main {
  margin-top: 20px;
}
</style>
