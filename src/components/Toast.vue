<template>
  <div
    class="toast"
    :style="{ display: showToast ? 'flex' : 'none' }"
    @click="$emit('update:show', false)"
  >
    {{ message }}
  </div>
</template>

<script>
export default {
  props: ["message", "show"],
  computed: {
    // Return given prop show.
    showToast() {
      return this.show;
    },
  },
  watch: {
    // Started a timeout to close toast when show is true.
    show() {
      setTimeout(() => {
        this.$emit("update:show", false);
      }, 2000);
    },
  },
};
</script>

<style scoped>
.toast {
  width: 250px;
  height: 50px;
  padding: 1rem;
  border-radius: 5px;
  position: fixed;
  top: 10px;
  right: 10px;
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 99;
}
</style>
