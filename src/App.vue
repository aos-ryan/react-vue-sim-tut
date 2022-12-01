<script setup>
import { ref } from 'vue';

import ProductDisplay from './components/ProductDisplay.vue'

// example of a react custom "hook" done in vue
// const useChangeWithDelay = function(state, newVal, delay) {
//   setTimeout(() => {
//     state.value = newVal
//   }, delay)
// };

const cart = ref([]);

const details = ref([
  {id: 1, desc: '50% cotton'}, 
  {id: 2, desc: '30% wool'}, 
  {id: 3, desc: '20% polyester'}]);

const removeFromCart = () => {
  if (cart.value.length >= 1) {
    cart.value.pop();
  }
};

const addToCart = function(id) {
  // console.log(id);
  cart.value.push(id);
};

</script>

<template>
  <div class="nav-bar"></div>
  <div class="cart">Cart ({{ cart.length }})
    <div class="remove-cart">
      <button 
      class="remove-button"
      v-on:click="removeFromCart"
      >Remove last item</button>
    </div>
  </div>
  <ProductDisplay :details='details' @add-to-cart="addToCart"></ProductDisplay>

</template>