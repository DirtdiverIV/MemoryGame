<template>
  <div>
    <div class="tablero">
      <CartaJuego
        v-for="(valor, index) in cartas"
        :key="index"
        :valor="valor"
        :mostrando="cartasMostradas.includes(index) || cartasEncontradas.includes(valor)"
        :encontrada="cartasEncontradas.includes(valor)"
        @clic="hacerClicEnCarta(index)"
      />
    </div>
    <div v-if="juegoCompletado">
      ¡Felicidades, has completado el juego!
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
      cartas: ['A', 'B', 'C', 'D', 'E', 'F', 'G', 'H', 'A', 'B', 'C', 'D', 'E', 'F', 'G', 'H'],
      cartasMostradas: [],
      cartasEncontradas: [],
      juegoCompletado: false
    };
  },
  methods: {
    hacerClicEnCarta(index) {
      if (!this.cartasMostradas.includes(index) && this.cartasMostradas.length < 2) {
        this.cartasMostradas.push(index);

        if (this.cartasMostradas.length === 2) {
          // Verificar si las cartas son iguales
          if (this.cartas[this.cartasMostradas[0]] === this.cartas[this.cartasMostradas[1]]) {
            // Las cartas son iguales, marcarlas como encontradas
            this.cartasEncontradas.push(this.cartas[this.cartasMostradas[0]]);
            
            // Verificar si todas las cartas han sido encontradas
            if (this.cartasEncontradas.length === this.cartas.length / 2) {
              this.juegoCompletado = true;
            }
          }

          // Ocultar las cartas después de un breve tiempo
          setTimeout(() => {
            this.cartasMostradas = [];
          }, 1000); // Ajusta el tiempo según tus preferencias
        }
      }
    }
  }
}
</script>

<style scoped>
/* Estilos específicos del juego de memoria */
.tablero {
  display: flex;
  flex-wrap: wrap;
}
</style>