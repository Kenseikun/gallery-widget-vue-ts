/** @author Sebastian Dziechciarz */
<template>
  <div class="gallery__content">
    <img
      :src="newUrlProp"
      alt=""
      class="gallery__image"
      :style="{
        filter: `grayscale(${imageGrayscale}%)`,
        opacity: `${imageOpacity}`,
      }"
    />
  </div>
</template>

<script lang="ts">
import { Vue, Prop, Component } from "vue-property-decorator";

@Component({})
export default class ImagesView extends Vue {
  @Prop({ type: String })
  public imageUrl!: string;

  @Prop({ type: String })
  public imageGrayscale!: string;

  @Prop({ type: String })
  public imageOpacity!: string;
}
</script>

<style lang="scss">
.gallery {
  &__content {
    position: relative;

    display: flex;
    justify-content: space-around;
    align-items: flex-end;

    height: 19rem;
    width: 100%;
  }

  &__image {
    box-shadow: 1px 1px 15px -2px #000000;

    object-fit: cover;

    width: 90%;
    height: 100%;

    border-radius: 10px;

    position: absolute;
    top: -20px;
    left: 50%;
    transform: translateX(-50%);
  }
}
</style>