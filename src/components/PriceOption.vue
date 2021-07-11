<template>
  <tr>
    <td>{{ item }}</td>
    <td v-for="(price, id) in getPrices(item)" :key="id">{{ price }}</td>
  </tr>
  <PriceOption
    v-for="(item, id) in getUniqOptions"
    :key="id"
    :item="item"
    :index="nextIndex"
    :variants="getrowList(item, index)"
    :prevVariants="variants"
  >
  </PriceOption>
</template>

<script>
export default {
  name: "PriceOption",
  props: ["index", "item", "variants", "prevVariants"],
  data() {
    return {
      nextIndex: this.index + 1
    };
  },

  methods: {
    getrowList(item, index) {
      return this.variants.filter(elem => {
        if (elem.options[index] == item) {
          return true;
        }
      });
    },

    getPrices(element) {
      // if first option (top lvl) take a first price
      let arr = [];
      if (this.index == 0) {
        
        this.variants[0].prices.forEach(item => {
          arr.push(item.price);
        });
        return arr;
      } else {
        this.prevVariants.forEach(option => {
             // Iterable element name is equal name in price object. 
          if (option.options[this.index] == element) {
            option.prices.forEach(price => arr.push(price.price));
          }

        });
        return arr;
      }
    },

    addPrev() {
      let arr = this.prevOptions.map(item => item);
      arr.push(this.item);
      return arr;
    }
  },

  computed: {
    getUniqOptions() {
      let arr = [];

      this.variants.forEach(item => {
        let element = item.options[this.nextIndex];
        if (!arr.includes(element)) {
          arr.push(element);
        }
      });

      return arr;
    }
  }
};
</script>
