<template>
  <div class="juego">
    <turno :turno-actual="turnoActual"></turno>
    <hr />
    <tablero
      @cambio-turno="cambioTurno"
      @ganado="ganado"
      @empatado="empatado"
      ref="tablero"
    >
    </tablero>
    <hr />
    <button @click="nuevoJuego">Nuevo Juego</button>
  </div>
</template>

<script>
import Turno from "../components/Turno.vue";
import Tablero from "../components/Tablero.vue";
export default {
  name: "Juego",
  components: {
    Turno,
    Tablero,
  },
  data: function() {
    return {
      turnoActual: "X",
    };
  },
  methods: {
    ganado(e) {
      setTimeout(
        function() {
          alert("Ganan las " + e.tokenActual);
        }.bind(this),
        1
      );
    },
    empatado() {
      setTimeout(
        function() {
          alert("Empate");
        }.bind(this),
        1
      );
    },
    cambioTurno(e) {
      this.turnoActual = e.tokenActual;
    },

    nuevoJuego() {
      this.$refs.tablero.nuevoJuego();
    },
  },
};
</script>

<style>
.juego {
  width: 350px;
  margin: auto;
  padding: 20px;
  background-color: #fafafa;
  box-shadow: 0px 0px 10px #141414;
}
</style>
