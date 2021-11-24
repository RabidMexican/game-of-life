<template>
  <div class="board" v-if="this.board !== null">
    <Tile
      v-for="(tile, i) in board"
      :key="i"
      :index="i"
      :boardSize="size"
      :alive="tile"
      :playing="playing"
      @toggle="toggleTileStatus(i)"
    />
  </div>
</template>

<script>
import { EventBus } from "../plugins/event-bus";
import Tile from "./Tile";

export default {
  name: "Board",
  components: { Tile },
  data() {
    return {
      size: 400,
      board: null,
      interval: null,
      playing: false,
    };
  },
  mounted() {
    EventBus.$on("play", this.play);
    EventBus.$on("stop", this.stop);
    EventBus.$on("reset", this.reset);
    EventBus.$on("size", (data) => {
      this.updateSize(data);
    });
    this.setup();
  },
  methods: {
    setup() {
      let data = [];
      for (let i = 0; i < this.size; i++) {
        let status = false;
        data[i] = status;
      }
      this.board = data;
    },
    update() {
      let newBoard = [];
      this.board.forEach((tile, index) => {
        newBoard[index] = this.getStatus(index);
      });
      this.board = [];
      this.board = newBoard;
    },
    play() {
      this.playing = true;
      this.interval = setInterval(() => {
        this.update();
      }, 1000);
    },
    stop() {
      this.playing = false;
      clearInterval(this.interval);
    },
    reset() {
      this.setup();
    },
    updateSize(value) {
      this.size = value;
      this.setup();
    },
    toggleTileStatus(index) {
      if (this.playing) return;
      let newBoard = this.board;
      newBoard[index] = !newBoard[index];
      this.board = [];
      this.board = newBoard;
    },
    getNeighborsForTile(index) {
      const line = Math.sqrt(this.size);
      const neighbors = [
        index - line - 1,
        index - line,
        index - line + 1,
        index - 1,
        index + 1,
        index + line - 1,
        index + line,
        index + line + 1,
      ];
      return this.wrapNeighbors(neighbors);
    },
    wrapNeighbors(neighbors) {
      let result = neighbors;
      neighbors.forEach((neighbor, i) => {
        if (neighbor > this.size - 1) result[i] = neighbor % this.size;
        else if (neighbor < 0) result[i] = this.size + neighbor;
      });
      return result;
    },
    getStatus(tile) {
      const neighbors = this.getNeighborsForTile(tile);
      const alive = this.board[tile];
      let countAlive = 0;
      neighbors.forEach((neighbor) => {
        if (this.board[neighbor] === true) {
          countAlive++;
        }
      });
      // 1. Any live cell with two or three live neighbours survives.
      if (alive && countAlive >= 2 && countAlive <= 3) return true;
      // 2. Any dead cell with three live neighbours becomes a live cell.
      if (!alive && countAlive == 3) return true;
      // 3 .All other live cells die in the next generation.
      if (alive) return false;
      // 4. All other dead cells stay dead.
      return false;
    },
  },
};
</script>

<style scoped>
.board {
  width: 334px;
  height: 334px;
  border: 0.5px solid black;
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
}
</style>
