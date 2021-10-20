<template>
  <div id="app">
    <main-header />
    <product-card v-for="(product, i) in allProducts" :key="i" :product="product" />
  </div>
</template>

<script>
import MainHeader from './components/MainHeader.vue'
import ProductCard from './components/ProductCard.vue'
import products from './products'

export default {
  name: 'App',
  components: {
    MainHeader,
    ProductCard,
  },
  data() {
    return {
      allProducts: [...products]
    }
  },
}
</script>

<style>
</style>
