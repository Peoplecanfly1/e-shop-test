<template>
  <div class="pricing">
    <h2>Pricing</h2>
    <table>
      <thead>
        <tr>
          <!-- Table header regions and currency -->
          <th class="th-name">Product</th>
          <th v-for="(item, index) in countries" :key="index">
            {{ item.name + ", " + item.currency }}
          </th>
        </tr>
      </thead>
      <tr>
        <!-- Poduct main price w/o options -->
        <td class="th-name">{{ product.name }}</td>
        <td v-for="(item, index) in priceList" :key="index">
          {{ item.price }}
        </td>
      </tr>
      <template v-if="product.options.length">
        <PriceOption
          v-for="(item, id) in getUniqOptions"
          :key="id"
          :item="item"
          :index="index"
          :variants="getrowList(item, index)"
        >
        </PriceOption>
      </template>
    </table>
  </div>
</template>

<script>
import PriceOption from "./PriceOption.vue";

export default {
  data() {
    return {
      index: 0,
      prevOptions: null
    };
  },

  components: {
    PriceOption
  },

  methods: {
    getrowList(item, index) {
      return this.product.variants.filter(elem => {
        if (elem.options[index] == item) {
          return true;
        }
      });
    }
  },

  computed: {
    priceList() {
      return this.product.variants[0].prices;
    },

    isntEmptyArr() {
      if (this.product.variants[0].options[this.index]) {
        return true;
      }

      return false;
    },

    getUniqOptions() {
      let arr = [];

      this.product.variants.forEach(item => {
        let element = item.options[this.index];
        if (!arr.includes(element)) {
          arr.push(element);
        }
      });

      return arr;
    }
  },

  props: ["product", "countries"]
};
</script>
