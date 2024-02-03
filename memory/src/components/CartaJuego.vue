<template>
  <div class="carta" @click="hacerClic">
    {{ mostrando ? valor : '?' }}
  </div>
</template>

<script>
export default {
  name: 'CartaJuego',
  props: ['valor', 'mostrando'],
  methods: {
    hacerClic() {
      // Lógica para manejar el clic de la carta
      this.$emit('clic', this.valor);
    }
  }
}
</script>

<style scoped>
/* Estilos específicos de la carta */
.carta {
  width: 100px;
  height: 100px;
  background-color: #ccc;
  display: flex;
  align-items: center;
  justify-content: center;
  margin: 5px;
  font-size: 18px;
  cursor: pointer;
}
</style>