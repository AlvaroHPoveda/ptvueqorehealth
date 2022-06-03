<template>
  <div>
    LE TOCA <span class="token">{{ turnoActual }}</span>
  </div>
</template>

<script>
export default {
  name: "Turno",
  props: {
    turnoActual: String,
  },
};
</script>

<style>
.token {
  font-size: 20px;
  background-color: #db0c0c;
  padding: 5px;
  border-radius: 20px;
}
</style>
