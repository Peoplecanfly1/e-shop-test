<template>
  <div class="wrapper">
    <header>
      <h1 class="logo">Scarlett</h1>
      <div class="breadcrumbs">
        <img src="./assets/Arrow.png" alt="arrow" />
        <h5>Back to Products</h5>
      </div>
    </header>
    <div class="publish">
      <h5>Last updated 4 hours ago</h5>
      <button class="button button_publish button_disabled">Publish</button>
    </div>
    <!-- Description of product incl Images -->
    <Description v-if="backData" :backData="backData"> </Description>

    <!-- Options & variants -->
    <Options v-if="backData" :products="backData.product"> </Options>
    <Pricing
      v-if="backData"
      :product="backData.product"
      :countries="backData.regions"
    >
    </Pricing>

    <button class="button button_light">
      <img src="./assets/Delete.png" alt="" />
      <p>Delete</p>
    </button>
  </div>
</template>

<script>
import Description from "./components/Description.vue";
import Options from "./components/Options.vue";
import Pricing from "./components/Pricing.vue";

export default {
  name: "App",
  components: { Description, Options, Pricing },
  data() {
    return {
      backData: null
    };
  },

  created: async function() {
    let result = await fetch("http://localhost:4000/api/products/rose");
    let response = await result.json();
    console.log(response);
    this.backData = response;
  }
};
</script>
