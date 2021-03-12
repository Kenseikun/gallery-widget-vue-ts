<template>
  <div id="app" class="app">
    <gallery-widget :widgetSize="widgetSize"></gallery-widget>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";

import GalleryWidget from "./gallery-widget/GalleryWidget.vue";

@Component({
  components: { GalleryWidget },
})
export default class App extends Vue {
  // Use prop small or large to change gallery
  public widgetSize: any = "large";
}
</script>

<style lang="scss">
@import url("https://fonts.googleapis.com/css2?family=Roboto:wght@300;500;700;900&display=swap");
.app {
  font-family: "Roboto", sans-serif;

  display: flex;
  justify-content: center;
  align-items: center;

  height: 100vh;
}
</style>
