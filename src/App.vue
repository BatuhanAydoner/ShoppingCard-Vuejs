<template>
  <div id="app">
    <main-header
      :productCount="productCount"
      :is-products-dialog-active.sync="isProductsDialogActive"
    />
    <b-container>
      <b-row>
        <product-card
          v-for="(product, i) in allProducts"
          :key="i"
          :product="product"
          @add-to-chart="addToChart"
        />
      </b-row>
      <products-dialog
        :isActive="isProductsDialogActive"
        :products="selectedProducts"
        @increment="increment"
        @decrement="decrement"
        @closedDialog="closedDialog"
      />
    </b-container>
  </div>
</template>

<script>
import MainHeader from "./components/MainHeader.vue";
import ProductCard from "./components/ProductCard.vue";
import ProductsDialog from "./components/ProductsDialog.vue";
import products from "./products";

export default {
  name: "App",
  components: {
    MainHeader,
    ProductCard,
    ProductsDialog,
  },
  data() {
    return {
      allProducts: [...products],
      selectedProducts: [],
      productCount: 0,
      isProductsDialogActive: false,
    };
  },
  methods: {
    addToChart(product) {
      let sameProduct = this.selectedProducts.find((item) => item.id === product.id);
      if (sameProduct) {
        const findedSize = sameProduct.sizes.find(
          (item) => item.number === product.sizes[0].number
        );
        if (findedSize) {
          findedSize.piece += product.sizes[0].piece;
        } else {
          sameProduct.sizes.push({
            number: product.sizes[0].number,
            piece: product.sizes[0].piece,
          });
        }

        sameProduct.piece += product.piece;
        sameProduct.price += product.price;
      } else {
        this.selectedProducts.push(product);
      }
      this.productCount += product.piece;
    },
    increment(product, number) {
      const size = product.sizes.find((item) => item.number === number);
      size.piece += 1;
      this.productCount += 1;
    },
    decrement(product, number) {
      const size = product.sizes.find((item) => item.number === number);
      size.piece -= 1;
      this.productCount -= 1;

      if (size.piece === 0) {
        product.sizes = product.sizes.filter((item) => item.number !== size.number);
      }
      if (product.sizes.length === 0) {
        this.selectedProducts = this.selectedProducts.filter(
          (item) => item.id !== product.id
        );
      }
    },
    closedDialog() {
      this.isProductsDialogActive = false;
    },
  },
};
</script>

<style></style>
