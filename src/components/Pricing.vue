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
    </table>
  </div>
</template>

<script>
export default {
  data() {
    return {};
  },

  methods: {},

  computed: {
    priceList() {
      return this.product.variants[0].prices;
    }
  },

  props: ["product", "countries"]
};
</script>
