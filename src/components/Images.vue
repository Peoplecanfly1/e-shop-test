<template>
  <div class="images">
    <div class="images__header">
      <h2>Images</h2>
    </div>
    <div class="images__pics">
      <div
        class="images__pics_product"
        id=""
        v-for="(pic, id) in pics"
        :key="id"
      >
        <img :src=pic.url alt="product" />
      </div>
    </div>
    <div class="images__drag"
        :class="{'images__drag_minimized': pics.length}"
    >
      <!-- images__drag_minimized -->
      <p class="images__drag__text">
        Drag and drop or browse to choose a file
      </p>
      <p class="images__drag__formats">JPEG, PNG, GIF, MP4 are allowed</p>
    </div>
  </div>
</template>

<script>
export default {
  props: ["pics"]
};
</script>
