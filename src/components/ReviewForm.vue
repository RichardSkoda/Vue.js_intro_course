<template>
  <form class="review-form" @submit.prevent="onSubmit">
    <h3>Leave a review</h3>
    <label for="name">Name:</label>
    <input id="name" v-model="name">

    <label for="review">Review:</label>      
    <textarea id="review" v-model="review"></textarea>

    <label for="rating">Rating:</label>
    <select id="rating" v-model.number="rating">
      <option>5</option>
      <option>4</option>
      <option>3</option>
      <option>2</option>
      <option>1</option>
    </select>

    <label for="recommend">Would you recommend this product?</label>
    <select id="recommend" v-model="recommend">
      <option>Yes</option>
      <option>No</option>
    </select>

    <input class="button" type="submit" value="Submit">
  </form>
</template>

<script setup lang="ts">
import { ref } from 'vue';

const emits = defineEmits<{
  (e: 'reviewsubmitted', id: object): void
}>()

const name = ref('')
const review = ref('')
const rating = ref(null)
const recommend = ref(null)

const onSubmit = () => {
  if (name.value === '' || review.value === '' || rating.value === null || recommend === null) {
    alert('Reviw is incomplete. Please fill out every field.')
  }else {
    let productReview = {
    name: name.value,
    review: review.value,
    rating: rating.value,
    recommend: recommend.value
  }
  emits('reviewsubmitted', productReview)
  }

  name.value = ''
  review.value = '',
  rating.value = null
  recommend.value = null
}


</script>

<style lang="scss" scoped>

</style>