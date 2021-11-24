<template>
  <v-card>
    <v-footer padless>
      <v-card flat tile width="100%" class="text-center">
        <v-card-text>
          {{ new Date().getFullYear() }} Ben Pocklington
        </v-card-text>
      </v-card>
    </v-footer>
  </v-card>
</template>

<script>
export default {
  name: "AppFooter",
};
</script>

