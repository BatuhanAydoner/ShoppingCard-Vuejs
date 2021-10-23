<template>
  <div class="header">
    <h1>ShoppingCard - Vue.js</h1>
    <transition name="move" appear>
      <div style="margin-right: 20px" @click="openDialog">
        <b-icon-cart-4 v-if="show" class="chart" />
        <b-badge v-if="productCount > 0" variant="light">{{ productCount }}</b-badge>
      </div>
    </transition>
  </div>
</template>

<script>
export default {
  props: ["productCount"],
  data() {
    return {
      show: true,
    };
  },
  methods: {
    // Emit true to show products dialog.
    openDialog() {
      this.$emit("update:is-products-dialog-active", true);
    },
  },
};
</script>

<style scoped>
.header {
  width: 100%;
  height: 50px;
  background: orange;
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.chart {
  font-size: 30px;
}

.move-enter-active {
  animation: move-chart 2s;
}
@keyframes move-chart {
  0% {
    transform: translateX(-600px);
  }
  100% {
    transform: translateX(0px) rotate(45deg);
  }
}
</style>
