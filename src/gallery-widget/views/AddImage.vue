/** @author Sebastian Dziechciarz */
<template>
  <div class="image--edit">
    <h2 v-if="urlInput === ''">Add your own image...</h2>
    <img
      :src="urlInput"
      alt=""
      :style="{
        width: 100 + 'px',
        filter: `grayscale(${grayscale}%)`,
        opacity: `${opacity}`,
      }"
    />

    <form class="form" @submit.prevent="submitData">
      <input
        class="form__input"
        name="addImage"
        type="text"
        placeholder="Add your image url ..."
        v-model="urlInput"
      />

      <label for="opacity">Opacity</label>
      <input
        type="range"
        name="opacity"
        value="1"
        min="0"
        step="0.1"
        max="1"
        v-model="opacity"
      />
      <p class="form__values">{{ opacity }}</p>

      <label for="grayscale">Grayscale</label>
      <input
        type="range"
        name="grayscale"
        value="0"
        min="0"
        step="1"
        max="100"
        v-model="grayscale"
      />
      <p class="form__values">{{ grayscale }}</p>
      <button
        class="form__btn"
        type="submit"
        :disabled="urlInput === '' ? true : false"
      >
        confirm
      </button>
    </form>
  </div>
</template>

<script lang="ts">
import { Vue, Component } from "vue-property-decorator";

const GRAY_SCALE_VALUE = "100";
const OPACITY_VALUE = "1";

@Component({})
export default class AddImage extends Vue {
  urlInput = "";
  opacity = OPACITY_VALUE;
  grayscale = GRAY_SCALE_VALUE;

  public submitData() {
    const newImage = {
      url: this.urlInput,
      filters: { opacity: this.opacity, grayscale: this.grayscale },
    };

    this.$emit("add-image", newImage);

    this.urlInput = "";
    this.opacity = OPACITY_VALUE;
    this.grayscale = GRAY_SCALE_VALUE;
  }
}
</script>

<style lang="scss">
.image--edit {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;

  color: #fff;
  width: 100%;
  height: 100%;

  .form {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;

    width: 100%;

    font-size: 0.8rem;
    margin: 10px auto;

    &__input {
      border: none;
      outline: none;
      border-radius: 10px;

      background-color: #3e295c;
      padding: 6px 6px;
      color: #fff;
      width: 80%;

      margin: 10px auto;
    }

    &__values {
      font-size: 0.8em;
    }

    &__btn {
      background-color: #cf439c;
      border: none;
      padding: 2px 20px;
      border-radius: 3px;
      margin: 10px auto 0px auto;

      font-size: 0.8rem;
      cursor: pointer;

      transition: 0.3s;

      &:hover:enabled {
        color: #fff;
      }
    }
  }
}
</style>