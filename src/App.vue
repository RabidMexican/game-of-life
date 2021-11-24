<template>
  <div id="app">
    <h1>Game of Life</h1>
    <board />
  </div>
</template>

<script>
import Board from "./components/Board";
export default {
  name: "App",
  components: { Board },
  props: {
    index: {
      require: true,
      type: Number,
    },
  },
};
</script>

<style>
</style>
