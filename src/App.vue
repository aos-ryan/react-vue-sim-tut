<script setup>
import { ref } from 'vue';
import socksGreenImage from './assets/images/socks_green.jpeg'

// example of a react custom "hook" done in vue
const useChangeWithDelay = function(state, newVal, delay) {
  setTimeout(() => {
    state.value = newVal
  }, delay)
}
const product = ref('Socks');
const image = ref(socksGreenImage)
const inStock = ref(true)

const details = ref(['50% cotton', '30% wool', '20% polyester'])
const variants = ref([
  { id: 2234, colour: 'green'},
  { id: 2235, colour: 'blue'}
])
</script>

<template>
  <div class="nav-bar"></div>
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
          <div v-for="variant in variants" :key="variant.id">{{ variant.colour }}</div>
        </div>
      </div>
    </div>
</template>