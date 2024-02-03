<template>
  <div @click="clicEnCarta" class="carta col-md-3 mb-4">
    <img v-if="mostrando || encontrada" :src="imagenSrc" alt="Carta" />
    <div v-else class="cubierta">
      <img src="@/assets/carta.png" alt="Cubierta" />
    </div>
  </div>
</template>

<script>
export default {
  props: {
    valor: String,
    mostrando: Boolean,
    encontrada: Boolean
  },
  methods: {
    clicEnCarta() {
      if (!this.mostrando && !this.encontrada) {
        this.$emit('clic');
      }
    }
  },
  computed: {
    imagenSrc() {
      return require(`@/assets/${this.valor}.png`);
    }
  }
};
</script>

<style scoped>
.carta {
  width: 128px;
  height: 128px;
  border: 1px solid #ccc;
  cursor: pointer;
  position: relative;
  margin: 0; /* Elimina el margen */
  padding: 0; /* Elimina el relleno */
}

img {
  width: 128px;
  height: 128px;
  object-fit: cover;
}

.cubierta img {
  width: 128px;
  height: 128px;
  object-fit: cover;
}

.cubierta img {
  max-width: 100%; /* Ajusta el tamaño de la imagen de la cubierta según sea necesario */
  max-height: 100%;
}
</style>