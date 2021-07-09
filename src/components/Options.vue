<template>
    <div class="wear-models">
      <section class="wear-models__option">
        <h2>Options</h2>
        <h5 class="wear-models__option_question">
          Does your product have options like color or size
        </h5>
        <div class="options options_first">
          <ul class="options__list" id="option">
            <li class="options__list__item ">
              <p>Color</p>
              <!-- <button>x</button> -->
            </li>
            <li class="options__list__item">
              <p>Size</p>
              <!-- <button>x</button> -->
            </li>
            <li class="options__list__item options__list__item__new">+New</li>
          </ul>
        </div>
      </section>
      <section class="wear-models__variants">
          <h2>Variants</h2>
      </section>
    </div>
</template>


<script>
export default {
    data(){
        return{
            options: this.products.options,
            variants: this.products.variants
        }
    },

   props: ['products']
}
</script>