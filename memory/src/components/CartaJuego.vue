<template>
  <div @click="clicEnCarta" class="carta col-md-3 mb-4">
    <img v-if="mostrando || encontrada" :src="imagenSrc" alt="Carta" />
    <div v-else class="cubierta"></div>
  </div>
</template>

<script>
export default {
  props: {
    valor: String,
    mostrando: Boolean,
    encontrada: Boolean
  },
  computed: {
    imagenSrc() {
      return require(`@/assets/${this.valor}.png`);
    }
  },
  methods: {
    clicEnCarta() {
      if (!this.mostrando && !this.encontrada) {
        this.$emit('clic');
      }
    }
  }
};
</script>

<style scoped>
.carta {
  width: 256px;
  height: 256px;
  border: 1px solid #ccc;
  cursor: pointer;
  position: relative;
}

img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.cubierta {
  width: 100%;
  height: 100%;
  background-color: #333;
}
</style>