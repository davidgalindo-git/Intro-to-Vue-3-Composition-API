<script setup>
import { ref } from 'vue'
import socksGreenImage from './assets/images/socks_green.jpeg'
import socksBlueImage from './assets/images/socks_blue.jpeg'

const product = ref('Socks')
const details = ref(['50% cotton', '30% wool', '20% polyester'])
const variants = ref([
  { id: 0, color: 'green', image: socksGreenImage, quantity: 10, onSale: true},
  { id: 1, color: 'blue', image: socksBlueImage, quantity: 0, onSale: false},
])
const cart = ref(0)
const brand = ref('CPNV')
const selectedVariant = ref(0)
const name = ref('')
const review = ref('')
const rating = ref(null)

function sale(){
  if (variants.value[selectedVariant.value].onSale) {
  return " est en action !"  }
}
function image() {
  return variants.value[selectedVariant.value].image
}
function inStock() {
  return variants.value[selectedVariant.value].quantity > 0
}
function addToCart() {
  cart.value++
}
function subtractFromCart() {
  if (cart.value > 0) {
    cart.value--
  }
}
function brandedProduct() {
  return brand.value + ' ' + product.value
}
function updateVariant(variantId) {
  selectedVariant.value = variantId
}
function onSubmit() {
  let productReview = {
    name: name.value,
    review: review.value,
    rating: rating.value}
  console.log(productReview)
}
</script>
  
<template>
  <div class="nav-bar"></div>
  <div class="cart">Cart({{ cart }})</div>
  <div class="product-display">
    <div class="product-container">
      <div class="product-image">    
        <img v-if="inStock()" v-bind:src="image()" alt="Socks"/>
        <img v-else v-bind:src="image()" alt="Socks" class="out-of-stock-img"/>
      </div>
      <div class="product-info">
        <h1>{{ brandedProduct() }}</h1>
        <p>{{ sale() }}</p>
        <p v-if="inStock()">In Stock</p>
        <p v-else>Out of Stock</p>
        <ul>
          <li v-for="detail in details">{{ detail }}</li>
        </ul>
        <div class="color-circle"
          v-for="variant in variants"
          :key="variant.id"
          :style="{ backgroundColor: variant.color }"
          @mouseover="updateVariant(variant.id)"
        >
        </div>
        <button v-if="inStock()" @click="addToCart()" >Ajouter</button>
        <button v-else class="disabledButton">Ajouter</button>
        <button @click="subtractFromCart()">Enlever du panier</button>

        <form class="review-form" @submit.prevent="onSubmit">
          <h3>Laissez un commentaire</h3>
          <label for="name">Nom:</label>
          <input id="name" v-model="name"/>

          <label for="review">Commentaire:</label>
          <textarea id="review" v-model="review"></textarea>
      
          <label for="rating">Note:</label>
          <select id="rating" v-model.number="rating">
            <option>5</option>
            <option>4</option>
            <option>3</option>
            <option>2</option>
            <option>1</option>
          </select>
      
          <input class="button" type="submit" value="Valider"/>
        </form>
        <p>{{ productReview }}</p>
      </div>
    </div>
  </div>
</template>