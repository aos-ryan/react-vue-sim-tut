<script setup>
import { ref } from 'vue';
import socksGreenImage from './assets/images/socks_green.jpeg'
import socksBlueImage from './assets/images/socks_blue.jpeg'

// example of a react custom "hook" done in vue
const useChangeWithDelay = function(state, newVal, delay) {
  setTimeout(() => {
    state.value = newVal
  }, delay)
};
const product = ref('Socks');
const image = ref(socksGreenImage);
const inStock = ref(true);

const details = ref(['50% cotton', '30% wool', '20% polyester'])
const variants = ref([
  { id: 2234, colour: 'green', image: socksGreenImage},
  { id: 2235, colour: 'blue', image: socksBlueImage}
]);

const cart = ref(0);
const addToCart = () => cart.value += 1

const updateImage = (variantImage) => {
  image.value = variantImage
}
</script>

<template>
  <div class="nav-bar"></div>
  <div class="cart">Cart ({{ cart }})</div>
    <div class="product-display">
      <div class="product-container">
        <div class="product-image">
          <!-- <img v-bind:src="image"> longform version -->
          <img :src="image">
        </div>
        <div class="product-info">
          <h1>{{ product }}</h1>
          <p v-if="inStock">In Stock</p>
          <p v-else>Out of Stock</p>
          <ul>
            <li v-for="detail in details">{{ detail }}</li>
          </ul>
          <div 
          v-for="variant in variants" 
          :key="variant.id" 
          @mouseover="updateImage(variant.image)"
          class="colour-circle"
          :style="{ backgroundColor: variant.colour}"
          >
        </div>
        </div>
        <button 
        class="button" 
        :class="{ disabledButton: !inStock }"
        v-on:click="addToCart"
        >Add to Cart</button>
      </div>
    </div>
</template>