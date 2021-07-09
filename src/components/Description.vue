<template>
  <main>
    <div class="description">
      <div class="description__header">
        <h2>Basics</h2>
        <ul class="lang">
          <li
            v-for="(lang, id) in backData.locales"
            :key="id"
            :class="{ 'not-active': currentLang != lang }"
            @click="currentLang = lang"
          >
            {{ getRegion(lang) }}
          </li>
        </ul>
      </div>
      <div class="description__input">
        <label>
          <p>Name</p>
          <input
            v-model="productName"
            type="text"
            name="name"
            id="name"
            placeholder="Scarlett"
          />
        </label>
        <label>
          <p>Description</p>
          <textarea
            v-model="productDescription"
            name="desc"
            id="desc"
            cols="30"
            rows="10"
            placeholder="Product description"
          ></textarea>
        </label>
      </div>
    </div>
    <Images :pics="productPics"> </Images>
  </main>
</template>

<script>
import Images from "./Images.vue";

export default {
  data() {
    return {
      currentLang: this.backData.locales[0], // firstLang as standart one.
      productName: this.backData.product.name,
      productDescription: this.backData.product.description,
      productPics: this.backData.product.images
    };
  },
  props: ["backData"],
  components: {
    Images
  },
  methods: {
    getRegion(str) {
      let result = str[0].toUpperCase() + str[1];
      return result;
    }
  }
};
</script>
