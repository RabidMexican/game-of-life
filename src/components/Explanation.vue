<template>
  <v-alert
    border="left"
    colored-border
    type="info"
    elevation="2"
    dismissible
    class="font-weight-light"
  >
    Use the controls below to play the Game of Life. Click on some squares to
    define them as "alive" and press play to see how their lives play out. You
    must stop the game in order to change the tiles, size or reset the board.
  </v-alert>
</template>

<script>
export default {
  name: "Explanation",
};
</script>

