<template>
  <div>
    <div class="container mt-5">
      <div class="row">
        <CartaJuego
          v-for="(valor, index) in cartas"
          :key="index"
          :valor="valor"
          :mostrando="cartasMostradas.includes(index) || cartasEncontradas.includes(valor)"
          :encontrada="cartasEncontradas.includes(valor)"
          @clic="hacerClicEnCarta(index)"
          class="col-md-3 mb-4"
        />
      </div>
      <div v-if="juegoCompletado" class="mt-3">
        ¡Felicidades, has completado el juego!
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
};
</script>