<script setup>
import { ref } from 'vue'

const data = ref({
  name: '',
  review: '',
  rating: null
});
const emit = defineEmits(['review-submitted']);

const onSubmit = () => {
  const productReview = {
    name: data.value.name,
    review: data.value.review,
    rating: data.value.rating,
  }
  emit('review-submitted', productReview)
  data.value.name = ''
  data.value.rating = ''
  data.value.review = null
};

</script>

<template>
  <form class="review-form" @submit.prevent="onSubmit">
    <h3>Leave a review</h3>
    <label for="name">Name:</label>
    <input id="name" v-model="data.name">

    <label for="review">Review:</label>      
    <textarea id="review" v-model="data.review"></textarea>

    <label for="rating">Rating:</label>
    <select id="rating" v-model="data.rating">
      <option>5</option>
      <option>4</option>
      <option>3</option>
      <option>2</option>
      <option>1</option>
    </select>

    <input class="button" type="submit" value="Submit">
  </form>
</template>