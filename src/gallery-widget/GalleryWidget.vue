/** @author Sebastian Dziechciarz */
<template>
  <div>
    <div class="gallery">
      <images-view
        v-if="(isVisible === 'gallery' && prop === 'small') || prop === 'large'"
        :imageUrl="imageUrlValue"
        :imageGrayscale="imageGrayscale"
        :imageOpacity="imageOpacity"
        :storedImages="storedImages"
      ></images-view>

      <keep-alive>
        <add-image
          v-if="isVisible === 'edit' && prop === 'small'"
          :storedImages="storedImages"
          @add-image="addImage"
        ></add-image>
      </keep-alive>

      <div v-if="prop === 'small'" class="gallery__buttons">
        <buttons-menu @gallery-visible="handleIsVisible"></buttons-menu>
      </div>
    </div>

    <div v-if="prop === 'large'" class="large">
      <keep-alive>
        <add-image
          :storedImages="storedImages"
          @add-image="addImage"
        ></add-image>
      </keep-alive>
    </div>
  </div>
</template>

<script lang="ts">
import { Component, Vue, Prop } from "vue-property-decorator";

import ImagesView from "./views/ImagesView.vue";
import ButtonsMenu from "./views/ButtonsMenu.vue";
import AddImage from "./views/AddImage.vue";

interface Image {
  url: string;
  filters: ImageFilters;
}

interface ImageFilters {
  opacity: string;
  grayscale: string;
}

@Component({
  components: {
    ImagesView,
    ButtonsMenu,
    AddImage,
  },
})
export default class GalleryWidget extends Vue {
  @Prop()
  public widgetSize!: string;

  constructor() {
    super();
    // this.widgetSize = "";
  }
  // public storedImages: Image[] = this.getImagesFromLocalStorage();
  public storedImages: Image[] = [
    {
      url:
        "https://i.pinimg.com/originals/2a/c8/6e/2ac86e24861ece6bd6c9c34208f12387.png",
      filters: { opacity: "1", grayscale: "100" },
    },
    {
      url:
        "https://i.graphicmama.com/blog/wp-content/uploads/2019/12/04164033/Futuristic-Vespa-black-and-orange-color-combinations-2020-example.jpg",
      filters: { opacity: "0.6", grayscale: "0" },
    },
  ];

  // TODO: HERE I NEED PROP INFORMATION "large" or "small"
  // prop = this.widgetSize;
  prop = "small";

  // Local storage | Start
  setImageToLocalStorage() {
    localStorage.setItem("GalleryWidget", JSON.stringify(this.storedImages));
  }

  getImagesFromLocalStorage() {
    let localStorageImages;

    if (localStorage.getItem("GalleryWidget")) {
      localStorageImages = JSON.parse(
        localStorage.getItem("GalleryWidget") || "0"
      );
    } else {
      localStorageImages = [];
    }

    return localStorageImages;
  }
  // Local storage | End

  // Switcher between gallery to add your image in small view by button click
  isVisible = "gallery";

  handleIsVisible(payload: string) {
    this.isVisible = payload;
  }

  addImage(payload: any) {
    this.storedImages = [...this.storedImages, payload];
    this.setImageToLocalStorage();
  }

  imageUrlValue = this.storedImages[0].url;
  imageGrayscale = this.storedImages[0].filters.grayscale;
  imageOpacity = this.storedImages[0].filters.opacity;

  created() {
    this.$emit("widget-mounted", "GalleryWidget", "GalleryWidget");

    this.getImagesFromLocalStorage();

    let counter = 0;

    setInterval(() => {
      if (counter < this.storedImages.length) {
        counter++;
        this.imageUrlValue = this.storedImages[counter].url;
        this.imageGrayscale = this.storedImages[counter].filters.grayscale;
        this.imageOpacity = this.storedImages[counter].filters.opacity;
      } else {
        counter = 0;
        this.imageUrlValue = this.storedImages[0].url;
        this.imageGrayscale = this.storedImages[0].filters.grayscale;
        this.imageOpacity = this.storedImages[0].filters.opacity;
      }
    }, 3000);
  }

  // counterIndex = 0;

  // mounted() {
  //   setInterval(() => {
  //     this.counterIndex++;
  //   }, 1000);
  // }

  // get itemIndex() {
  //   return this.counterIndex % this.storedImages.length;
  // }

  // get itemByIndex() {
  //   return this.storedImages[this.itemIndex];
  // }
}
</script>

<style lang="scss">
@import url("https://fonts.googleapis.com/css2?family=Roboto:wght@300;400;500;700&display=swap");
.gallery {
  * {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }

  font-family: "Roboto", sans-serif;
  background-color: #1a224b;
  box-shadow: 1px 1px 15px -2px #000000;

  width: 19rem;
  height: 19rem;

  display: flex;
  justify-content: center;
  align-items: flex-end;

  flex-direction: column;

  transition: 0.3s;
}
.gallery__buttons {
  display: flex;
  justify-content: center;
  align-items: flex-end;

  height: 10%;
  width: 100%;
}

.large {
  box-shadow: 1px 1px 15px -2px #000000;

  width: 19rem;
  height: 19rem;

  background-color: #1a224b;
}
</style>