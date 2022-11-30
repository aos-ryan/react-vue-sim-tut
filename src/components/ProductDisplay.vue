<script setup>
import { ref, computed } from 'vue'
import socksGreenImage from '../assets/images/socks_green.jpeg'
import socksBlueImage from '../assets/images/socks_blue.jpeg'
defineProps({
  details: {
  type: Array,
  required: true
  }
});

const product = ref('Socks');
const selectedVariant = ref(0);
const brand = ref('Kidd Classic')



const sizes = ref([
  { id: 1, desc: 'small'}, 
  { id: 2, desc: 'medium'}, 
  { id: 3, desc: 'large'}]);

const variants = ref([
  { id: 2234, colour: 'green', image: socksGreenImage, quantity: 0, onSale: false},
  { id: 2235, colour: 'blue', image: socksBlueImage, quantity: 50, onSale: true}
]);

const cart = ref(0);
const addToCart = () => cart.value += 1

const updateVariant = (index) => {
  selectedVariant.value = index
};

const title = computed(() => {
  if (onSale.value) {
    return brand.value + ' ' + product.value + ' -  On Sale!'
  }
  return brand.value + ' ' + product.value
});

const image = computed(() => {
  return variants.value[selectedVariant.value].image
});

const inStock = computed(() => {
  return variants.value[selectedVariant.value].quantity
});

const onSale = computed(() => {
  return variants.value[selectedVariant.value].onSale 
});

</script>

<template>
      <div class="product-display">
      <div class="product-container">
        <div class="product-image">
          <!-- <img v-bind:src="image"> longform version -->
          <img :class="{ 'out-of-stock-img': !inStock }" :src="image">
        </div>
        <div class="product-info">
          <h1>{{ title }}</h1>
          <p v-if="inStock">In Stock</p>
          <p v-else>Out of Stock</p>
          <ul>
            <li 
            v-for="detail in details"
            :key="detail.id"
            >{{ detail.desc }}</li>
          </ul>
          <ul>
            <li 
            v-for="size in sizes"
            :key="size.id"
            >{{ size.desc }}</li>
          </ul>
          <div 
          v-for="(variant, index) in variants" 
          :key="variant.id" 
          @mouseover="updateVariant(index)"
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