<template>
  <div>
    <div class="container mt-5">
      <div class="row">
        <CartaJuego
          v-for="(valor, index) in cartasMezcladas"
          :key="index"
          :valor="valor"
          :mostrando="cartasMostradas.includes(index) || cartasEncontradas.includes(valor)"
          :encontrada="cartasEncontradas.includes(valor)"
          @clic="hacerClicEnCarta(index)"
          class="col-md-3 mb-4"
        />
      </div>
      <div v-if="juegoCompletado" class="mt-3">
        <p :style="{ fontSize: juegoCompletado ? '24px' : 'inherit', fontWeight: juegoCompletado ? 'bold' : 'normal', color: juegoCompletado ? '#ffffff' : '#000000' }">
          ¡Felicidades, has completado el juego en {{ tiempoTranscurrido }} segundos!
        </p>
        <button v-if="juegoCompletado" @click="reiniciarJuego" class="btn btn-primary" style="background-color: #3a1c3d;">Volver a Empezar</button>
      </div>
    </div>
  </div>
</template>

<script>
import CartaJuego from './CartaJuego.vue';

export default {
  components: {
    CartaJuego
  },
  data() {
    return {
      cartas: ['A', 'B', 'C', 'D', 'E', 'F', 'G', 'H', 'I', 'J', 'K', 'L', 'M', 'N', 'O', 'A', 'B', 'C', 'D', 'E', 'F', 'G', 'H', 'I', 'J', 'K', 'L', 'M', 'N', 'O'],
      cartasMezcladas: [],
      cartasMostradas: [],
      cartasEncontradas: [],
      juegoCompletado: false,
      tiempoInicio: null,
      tiempoTranscurrido: 0
    };
  },
  mounted() {
    this.mezclarCartas();
    this.iniciarContadorTiempo();
  },
  methods: {
    hacerClicEnCarta(index) {
      if (!this.cartasMostradas.includes(index) && this.cartasMostradas.length < 2) {
        this.cartasMostradas.push(index);

        if (this.cartasMostradas.length === 2) {
          if (this.cartasMezcladas[this.cartasMostradas[0]] === this.cartasMezcladas[this.cartasMostradas[1]]) {
            this.cartasEncontradas.push(this.cartasMezcladas[this.cartasMostradas[0]]);
            
            if (this.cartasEncontradas.length === this.cartasMezcladas.length / 2) {
              this.juegoCompletado = true;
              this.detenerContadorTiempo();
            }
          }

          setTimeout(() => {
            this.cartasMostradas = [];
          }, 1000);
        }
      }
    },
    reiniciarJuego() {
      this.juegoCompletado = false;
      this.cartasMostradas = [];
      this.cartasEncontradas = [];
      this.mezclarCartas();
      this.iniciarContadorTiempo();
    },
    mezclarCartas() {
      // Clonar y mezclar el array de cartas
      this.cartasMezcladas = [...this.cartas].sort(() => Math.random() - 0.5);
    },
    iniciarContadorTiempo() {
      this.tiempoInicio = new Date();
      this.actualizarContadorTiempo();
    },
    detenerContadorTiempo() {
      this.tiempoTranscurrido = Math.floor((new Date() - this.tiempoInicio) / 1000);
    },
    actualizarContadorTiempo() {
      setInterval(() => {
        if (!this.juegoCompletado) {
          this.tiempoTranscurrido = Math.floor((new Date() - this.tiempoInicio) / 1000);
        }
      }, 1000);
    }
  }
};
</script>