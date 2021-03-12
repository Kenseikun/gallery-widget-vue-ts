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
  public widgetSize: any = "small";
}
</script>

<style lang="scss">
.app {
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>
