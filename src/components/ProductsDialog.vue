<template>
  <b-modal
    id="products-dialog"
    :visible="isActive"
    scrollable
    centered
    title="Selected Products"
    @hidden="closeDialog"
  >
    <div v-if="products.length === 0">There is no selected product.</div>
    <b-row v-for="product in products" :key="product.id">
      <b-col cols="4" class="d-flex align-items-start">
        <b-card-img :src="product.image" alt="Image" class="rounded-0"></b-card-img>
      </b-col>
      <b-col cols="8">
        <h6>{{ product.name }}</h6>
        <div v-for="size in product.sizes" :key="size.number">
          <div v-if="size.piece > 0">
            <span>Size: {{ size.number }} x {{ size.piece }}</span>
            <button class="btn-decrement" @click="decrement(product, size.number)">
              -
            </button>
            <button class="btn-increment" @click="increment(product, size.number)">
              +
            </button>
            <button class="btn-delete" @click="deleteShoe(product, size.number)">
              <b-icon-trash></b-icon-trash>
            </button>
          </div>
        </div>
        <hr />
      </b-col>
    </b-row>
  </b-modal>
</template>

<script>
export default {
  props: {
    isActive: {
      type: Boolean,
      required: true,
    },
    products: {
      type: Array,
      required: true,
    },
  },
  methods: {
    // Emit given product and numbe to increase current shoe piece.
    increment(product, number) {
      this.$emit("increment", product, number);
    },
    // Emit given product and numbe to decrease current shoe piece.
    decrement(product, number) {
      this.$emit("decrement", product, number);
    },
    deleteShoe(product, number) {
      this.$emit("delete-shoe", product, number);
    },
    // Close this dialog.
    closeDialog() {
      this.$emit("closedDialog", false);
    },
  },
};
</script>
