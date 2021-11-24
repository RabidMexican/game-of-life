<template>
  <div
    class="tile hover:"
    :style="{ height: size + '%', width: size + '%' }"
    v-bind:class="{ alive: alive, playing: playing }"
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
    playing: {
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
  border: 1px solid black;
  box-sizing: border-box;
  background-color: #2e2e2e;
}
.tile:hover {
  cursor: pointer;
}
.alive {
  background-color: #0cce26;
}
.playing {
  border: none;
}
.playing:hover {
  cursor: not-allowed;
}
</style>
