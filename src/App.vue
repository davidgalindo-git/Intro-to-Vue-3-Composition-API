<script setup>
import { ref } from 'vue'
import ProductDisplay from './components/ProductDisplay.vue'

const cart = ref(0)
const premium = ref(1)

function addToCart() {
  cart.value++
}
function subtractFromCart() {
  if (cart.value > 0) {
    cart.value--
  }
}
</script>
<template>
  <div class="nav-bar"></div>
  <div class="cart">Cart({{ cart }})</div>
  <ProductDisplay :premium="premium"> </ProductDisplay>
</template>