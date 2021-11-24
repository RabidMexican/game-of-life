<template>
  <div
    class="tile"
    :style="{ height: size + '%', width: size + '%' }"
    v-bind:class="{ alive: alive }"
    @click="$emit('toggle')"
  />
</template>

<script>
export default {
  name: "Tile",
  props: {
    index: {
      require: true,
      type: Number,
    },
    boardSize: {
      require: true,
      type: Number,
    },
    alive: {
      require: true,
      type: Boolean,
    },
  },
  computed: {
    size() {
      return 100 / Math.sqrt(this.boardSize);
    },
  },
};
</script>

<style scoped>
.tile {
  border: 0.5px solid black;
  box-sizing: border-box;
}
.alive {
  background-color: #000000;
}
</style>
