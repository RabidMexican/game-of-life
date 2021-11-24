<template>
  <v-card outline>
    <v-card-title>Controls</v-card-title>
    <v-card-text>
      Use the controls below to play the Game of Life. Click on some squares to
      define it as "alive" and press play to see the results. You must stop the
      game in order to change the tiles, or reset the board.
    </v-card-text>
    <v-card-actions>
      <v-btn @click="play" :disabled="playing" color="success" text>
        PLAY
      </v-btn>
      <v-btn @click="stop" :disabled="!playing" color="error" text>
        STOP
      </v-btn>
      <v-btn @click="reset" :disabled="playing" color="warning" text>
        RESET
      </v-btn>
    </v-card-actions>
  </v-card>
</template>

<script>
import { EventBus } from "../plugins/event-bus";
export default {
  name: "ControlPanel",
  data() {
    return {
      playing: false,
    };
  },
  methods: {
    play() {
      EventBus.$emit("play");
      this.playing = true;
    },
    stop() {
      EventBus.$emit("stop");
      this.playing = false;
    },
    reset() {
      EventBus.$emit("reset");
    },
  },
};
</script>

