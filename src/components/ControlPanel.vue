<template>
  <v-card outline>
    <v-card-title>Control Panel</v-card-title>
    <v-divider />
    <v-card-subtitle>Grid Size</v-card-subtitle>
    <v-card-text>
      <v-slider
        v-model="size"
        @change="updateSize"
        :tick-labels="labels"
        :max="2"
        :disabled="playing"
        step="1"
        ticks="always"
        tick-size="4"
      />
    </v-card-text>
    <v-divider />
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
      size: 1,
      labels: [100, 400, 1600],
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
    updateSize() {
      EventBus.$emit("size", this.labels[this.size]);
    },
  },
};
</script>

