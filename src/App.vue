<template>
  <v-app>
    <AppHeader />
    <v-main>
      <v-container>
        <v-row>
          <v-col fill-height>
            <ControlPanel />
          </v-col>
          <v-col>
            <Board />
          </v-col>
        </v-row>
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
import AppHeader from "./components/AppHeader";
import ControlPanel from "./components/ControlPanel";
import Board from "./components/Board";

export default {
  name: "App",
  components: { AppHeader, ControlPanel, Board },
};
</script>

<style>
.main {
  display: flex;
  flex-direction: row;
}
</style>