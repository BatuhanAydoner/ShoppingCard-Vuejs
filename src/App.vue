<template>
  <div id="app">
    <main-header />
    <product-card />
  </div>
</template>

<script>
import MainHeader from './components/MainHeader.vue'
import ProductCard from './components/ProductCard.vue'

export default {
  name: 'App',
  components: {
    MainHeader,
    ProductCard,
  }
}
</script>

<style>
</style>
