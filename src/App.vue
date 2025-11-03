<script setup>
import { ref } from 'vue'
import socksGreenImage from './assets/images/socks_green.jpeg'
import socksBlueImage from './assets/images/socks_blue.jpeg'

const product = ref('Socks')
const image = ref(socksGreenImage)
const inStock = false
  
const details = ref(['50% cotton', '30% wool', '20% polyester'])

const variants = ref([
  { id: 2234, color: 'green', image: socksGreenImage },
  { id: 2235, color: 'blue', image: socksBlueImage},
])

const cart = ref(0)

function addToCart() {
  cart.value++
}

function subtractFromCart() {
  if (cart.value > 0) {
    cart.value--
  }
}

function changeImage(itemPath) {
 image.value = itemPath
}

</script>
  
<template>
  <div class="nav-bar"></div>
  <div class="cart">Cart({{ cart }})</div>
  <div class="product-display">
    <div class="product-container">
      <div class="product-image">    
        <img v-if="inStock" v-bind:src="image" alt="Socks"/>
        <img v-else="inStock" v-bind:src="image" alt="Socks" class="out-of-stock-img"/>

      </div>
      <div class="product-info">
        <h1>{{ product }}</h1>
        <p v-if="inStock">In Stock</p>
        <p v-else>Out of Stock</p>
        <ul>
          <li v-for="detail in details">{{ detail }}</li>
        </ul>
        <div class="color-circle"
          @mouseover="changeImage(variant.image)"
          v-for="variant in variants"
          :key="variant.id"
          :style="{ backgroundColor: variant.color }"
          
        >
        </div>
        <button v-if="inStock==true" @click="addToCart()" >Ajouter</button>
        <button v-else class="disabledButton">Ajouter</button>
        <button @click="subtractFromCart()">Enlever du panier</button>
      </div>
    </div>
  </div>
</template>