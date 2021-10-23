<template>
  <div id="app">
    <toast message="Sepetinize ürün eklendi." :show.sync="showToast" />
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
          @add-to-chart="addToChard"
        />
      </b-row>
      <products-dialog
        :isActive="isProductsDialogActive"
        :products="selectedProducts"
        @increment="increment"
        @decrement="decrement"
        @delete-shoe="deleteShoe"
        @closedDialog="closedDialog"
      />
    </b-container>
  </div>
</template>

<script>
import MainHeader from "./components/MainHeader.vue";
import ProductCard from "./components/ProductCard.vue";
import ProductsDialog from "./components/ProductsDialog.vue";
import Toast from "./components/Toast.vue";
import products from "./data/products";

export default {
  name: "App",
  components: {
    MainHeader,
    ProductCard,
    ProductsDialog,
    Toast,
  },
  data() {
    return {
      allProducts: [...products], // All products from json file.
      selectedProducts: [], // Selected products list.
      productCount: 0, // Total selected product count.
      isProductsDialogActive: false, // Show or hide product dialog.
      showToast: false, // Showed when any product is added.
    };
  },
  methods: {
    /**
     * Add products to list
     * @param {Object} product - Product at selectedProducts array
     */
    addToChard(product) {
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
      this.showToast = true;
    },
    /**
     *   Increase given product' s piece.
     *   @param {Object} product - Product at selectedProducts array
     *   @param {Number} number - Size at given product' s sizes
     */
    increment(product, number) {
      const size = product.sizes.find((item) => item.number === number);
      size.piece += 1;
      this.productCount += 1;
    },
    /**
     *   Decrease given product' s piece.
     *   @param {Object} product - Product at selectedProducts array
     *   @param {Number} number - Size at given product' s sizes
     */
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
    /**
     *   Delete shoe from given product
     *   @param {Object} product - Product at selectedProducts array
     *   @param {Number} number - Size at given product' s sizes
     */
    deleteShoe(product, number) {
      this.productCount -= parseInt(
        product.sizes.find((item) => item.number === number).piece
      );
      product.sizes = product.sizes.filter((item) => item.number !== number);
      if (product.sizes.length === 0) {
        this.selectedProducts = this.selectedProducts.filter(
          (item) => item.id !== product.id
        );
      }
    },
    // Close products dialog.
    closedDialog() {
      this.isProductsDialogActive = false;
    },
  },
};
</script>

<style></style>
