<template>
    <div class="header">
        <h1>BatuExpress</h1>
        <transition name="move" appear>
            <b-icon-cart-4 v-if="show" class="chart"/>
        </transition>
    </div>
</template>

<script>
import {BIconCart4} from 'bootstrap-vue'
export default {
    components: {
        BIconCart4,
    },
    data() {
        return {
            show: true
        }
    }
}
</script>

<style scoped>
.header {
    width: 100%;
    height: 50px;
    background: rgb(111, 111, 255);
    display: flex;
    justify-content: space-between;
    align-items: center;
}

.chart {
    font-size: 30px;
    margin-right: 20px;
}

.move-enter-active {
  animation: move-chart 3s;
  animation-delay: 1s;
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