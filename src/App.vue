<template>
  <div id="app">
    <main-header :productCount="productCount" />
    <product-card
      v-for="(product, i) in allProducts"
      :key="i"
      :product="product"
      @add-to-chart="addToChart"
    />
  </div>
</template>

<script>
import MainHeader from "./components/MainHeader.vue";
import ProductCard from "./components/ProductCard.vue";
import products from "./products";

export default {
  name: "App",
  components: {
    MainHeader,
    ProductCard,
  },
  data() {
    return {
      allProducts: [...products],
      selectedProducts: [],
      productCount: 0,
    };
  },
  methods: {
    addToChart(product) {
      let sameProduct = this.selectedProducts.find(
        (item) => item.id === product.id && item.size === product.size
      );
      if (sameProduct) {
        sameProduct.piece += product.piece;
        sameProduct.price += product.price;
      } else {
        this.selectedProducts.push(product);
      }
      this.productCount += product.piece;
    },
  },
};
</script>

<style></style>
