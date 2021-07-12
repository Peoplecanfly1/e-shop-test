<template>
  <div class="wrapper">
    <header>
      <h1 class="logo">Scarlett</h1>
      <div class="breadcrumbs">
        <a href="">
          <img src="./assets/Arrow.png" alt="arrow" />
          <h5>Back to Products</h5>
        </a>
      </div>
    </header>
    <div class="publish">
      <h5>Last updated 4 hours ago</h5>
      <button
        class="button button_publish"
        :class="{ button_disabled: notChanged }"
        @click="sendProduct"
      >
        Publish
      </button>
    </div>
    <!-- Description of product incl Images -->
    <Description
      v-if="backData"
      :backData="backData"
      @changeName="changeBackName"
      @changeDesc="changeBackDesc"
    >
    </Description>

    <!-- Options & variants -->
    <Options v-if="backData" :products="backData.product"> </Options>

    <!-- Prining table -->
    <Pricing
      v-if="backData"
      :product="backData.product"
      :countries="backData.regions"
    >
    </Pricing>
    <Modal> </Modal>
    

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
import Modal from "./components/Modal.vue"

export default {
  name: "App",
  data() {
    return {
      backData: null,
      notChanged: true
    };
  },
  watch: {
    backData: {
      handler: function(val, oldVal) {
        if (oldVal != null) {
          this.notChanged = false;
        }
      },
      deep: true,
    }
  },
  components: { Description, Options, Pricing, Modal },

  created: async function() {
    let result = await fetch("http://localhost:4000/api/products/rose");
    let response = await result.json();
    this.backData = response;
    console.log(response);
  },

  methods: {
    changeBackName(name, lang) {
      if (lang == "en") {
        this.backData.product.name = name;
      } else {
        this.backData.product.localization[lang].name = name;
      }
    },

    changeBackDesc(desc, lang) {
      if (lang == "en") {
        this.backData.product.description = desc;
      } else {
        this.backData.product.localization[lang].description = desc;
      }
    },

    async sendProduct(){
      
        let request = await fetch("http://localhost:4000/api/products/rose", {
          method: "POST",
          headers: {
            'Content-Type': 'application/json;charset=utf-8'
          }, 
          body: JSON.stringify(this.backData)
        })

    },
  }
};
</script>
