<template>
  <div class="wear-models">
    <section class="wear-models__option">
      <h2>Options</h2>
      <h5 v-if="!options.length" class="wear-models__option_question">
        Does your product have options like color or size
      </h5>
      <div class="options options_first">
        <ul class="options__list" id="option">
          <li
            v-for="(option, index) in products.options"
            :key="index"
            class="options__list__item "
          >
            <p>{{ option }}</p>
            <button>x</button>
          </li>
          <li class="options__list__item options__list__item__new">+New</li>
        </ul>
      </div>
      <template v-if="options.length">
        <div class="options" v-for="(variant, index) in structuredVariants" :key="index" :id="index">
          <p>{{ index }}</p>
          <ul class="options__list" >
            <li class="options__list__item options__list__item_active"
                v-for="(item,indexx) in variant" :key="indexx"
            >
              <p>{{item}}</p>
              <button :id="item">x</button>
            </li>
           
            <li class="options__list__item options__list__item__new">+New</li>
          </ul>
        </div>
      </template>
    </section>
    <section v-if="options.length" class="wear-models__variants">
      <h2>Variants</h2>
      <ul class="options__list" id="variant">
        <li
          v-for="(variant, index) in variants"
          :key="index"
          class="options__list__item "
        >
          <p>{{ variant.options.join(" ") }}</p>
          <button>x</button>
        </li>
      </ul>
    </section>
  </div>
</template>

<script>
export default {
  props: ["products"],
  data() {
    return {
      options: this.products.options,
      variants: this.products.variants,
      structuredVariants: this.getColorList(this.products.options,this.products.variants)
    };
  },

  methods:{
      getColorList(options, variants){
          let len = options.length
          let result = {}
          for(let i = 0; i < len; i++){
              let variantsArr = []
              for(let j =0; j < variants.length; j++){
                let item =variants[j].options[i]
                if(!variantsArr.includes(item)){
                    variantsArr.push(item)
                }
              }
              result[options[i]] = variantsArr
          }
          return result
      }


  },

  
};
</script>
