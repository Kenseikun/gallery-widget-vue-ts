/** @author Sebastian Dziechciarz */
<template>
  <div>
    <button
      @click="setSelectedTab('gallery')"
      class="gallery__btn"
      :disabled="galleryVisible === 'gallery' ? true : false"
    >
      Gallery
    </button>

    <button
      @click="setSelectedTab('edit')"
      class="gallery__btn"
      :disabled="galleryVisible === 'edit' ? true : false"
    >
      Edit
    </button>
  </div>
</template>

<script lang="ts">
import { Vue, Component } from "vue-property-decorator";

import ImagesView from "../views/ImagesView.vue";
import AddImage from "../views/AddImage.vue";

@Component({
  components: {
    ImagesView,
    AddImage,
  },
})
export default class ButtonsMenu extends Vue {
  galleryVisible = "gallery";

  public setSelectedTab(tab: string) {
    this.galleryVisible = tab;
    this.$emit("gallery-visible", this.galleryVisible);
  }
}
</script>

<style lang="scss">
.gallery {
  .gallery__btn {
    cursor: pointer;

    text-transform: uppercase;

    width: 120px;
    border: none;
    outline: none;
    border-radius: 8px;
    background-color: #4bd5cf;

    padding: 8px 30px;
    margin: 6px 6px;

    transition: 0.3s;
    &:hover:enabled {
      color: #fff;
    }
  }
}
</style>