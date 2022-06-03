<template>
  <table>
    <tr v-for="(n, i) in 3" :key="i">
      <td v-for="(n, j) in 3" :key="j">
        <casilla
          :token-actual="tokenActual"
          :ref="'casilla' + i + j"
          @jugado="jugar"
          :fila="i"
          :col="j"
        >
        </casilla>
      </td>
    </tr>
  </table>
</template>

<script>
import Casilla from "./Casilla.vue";
export default {
  name: "Tablero",
  components: {
    Casilla,
  },
  data: function() {
    return {
      tokenActual: "X",
      matriz: [
        ["", "", ""],
        ["", "", ""],
        ["", "", ""],
      ],
    };
  },
  methods: {
    jugar(e) {
      this.matriz[e.fila][e.col] = this.tokenJugado;
      if (this.verificar(e.tokenJugado)) {
        this.$emit("ganado", this);
      } else if (this.verificarEmpate()) {
        this.$emit("empatado", this);
      } else {
        this.tokenActual = e.tokenJugado == "X" ? "O" : "X";
        this.$emit("cambio-turno", this);
      }
    },
    verificar(token) {
      for (let pos = 0; pos < 3; pos++) {
        if (
          this.matriz[pos][0] == token &&
          this.matriz[pos][1] == token &&
          this.matriz[pos][2] == token
        ) {
          return true;
        }
        if (
          this.matriz[0][pos] == token &&
          this.matriz[1][pos] == token &&
          this.matriz[2][pos] == token
        ) {
          return true;
        }
      }
      if (
        this.matriz[0][0] == token &&
        this.matriz[1][1] == token &&
        this.matriz[2][2] == token
      ) {
        return true;
      }
      if (
        this.matriz[0][2] == token &&
        this.matriz[1][1] == token &&
        this.matriz[2][0] == token
      ) {
        return true;
      }
      return false;
    },
    verificarEmpate() {
      const matrizTmp = this.matriz
        .join(",")
        .split(",")
        .join("");
      return matrizTmp.length == 9;
    },
    nuevoJuego() {
      for (let fila = 0; fila < 3; fila++) {
        for (let col = 0; col < 3; col++) {
          this.matriz[fila][col] = "";
          this.$refs["casilla" + fila + col][0].reiniciar();
        }
      }
    },
  },
};
</script>

<style>
table {
  margin: auto;
  border-collapse: collapse;
}
table td {
  border: 1px solid #000;
  width: 60px;
  height: 60px;
}
</style>
