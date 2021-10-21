<template>
  <b-card no-body class="overflow-hidden product-card" style="max-width: 580px">
    <b-row no-gutters>
      <b-col md="6" class="d-flex align-items-center">
        <b-card-img
          src="https://png.pngitem.com/pimgs/s/244-2441637_campus-shoes-png-transparent-png.png"
          alt="Image"
          class="rounded-0"
        ></b-card-img>
      </b-col>
      <b-col md="6">
        <b-card-body>
          <b-card-text>{{ product.category }}</b-card-text>
          <b-card-title title-tag="h4">{{ product.name }}</b-card-title>
          <b-card-title title-tag="h1">${{ product.price }}</b-card-title>
          <b-card-text>
            {{ product.description }}
          </b-card-text>
          <b-form-rating
            id="rating-10"
            :value="product.rating"
            :stars="5"
            size="sm"
            no-border
            readonly
          ></b-form-rating>
        </b-card-body>
      </b-col>
      <b-col md="6">
        <b-form-radio-group
          :options="product.sizes"
          class="general"
          v-model="selectedSize"
          buttons
          button-variant="success"
        ></b-form-radio-group>
      </b-col>
      <b-col md="2">
        <b-form-select
          v-model="selectedCount"
          :options="countOptions"
          size="sm"
          class="select-count"
        ></b-form-select>
      </b-col>
      <b-col md="4">
        <b-button @click="addToChart">ADD TO BASKET</b-button>
      </b-col>
    </b-row>
  </b-card>
</template>

<script>
export default {
  props: {
    product: {
      type: Object,
      required: true,
    },
  },
  data() {
    return {
      selectedSize: this.product.sizes[0],
      selectedCount: 1,
      countOptions: [1, 2, 3, 4, 5, 6, 7, 8, 9, 10],
    };
  },
  methods: {
    addToChart() {
      let indexOfSize = this.product.sizes
        .map((item) => item.value)
        .indexOf(this.selectedSize);
      let newProduct = {
        id: this.product.id,
        name: this.product.name,
        size: this.selectedSize,
        price: this.product.price + indexOfSize * 10,
        piece: this.selectedCount,
        image: this.product.image,
      };
      this.$emit("add-to-chart", newProduct);
      this.selectedSize = null
    },
  },
};
</script>

<style>
.product-card {
  padding: 1rem;
  border: 1px solid #888888 !important;
  box-shadow: 0px 0px 5px #888888;
}

.select-count {
  border: none;
  outline: none;
}

.general {
  position: relative;
  gap: 5px;
}

.general label {
  background: white;
  color: black;
}

.general label input {
  visibility: hidden !important;
  position: absolute !important;
}
</style>
