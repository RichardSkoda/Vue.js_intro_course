<template>
    <div class="product-display">
      <div class="product-container">
        <div
          class="product-image"
          :class="{ 'out-of-stock-img': !inStock }"
        >
          <img :src="image">
        </div>
        <div class="product-info">
          <h1>{{ title }}</h1>
          <p v-if="inStock">In Stock</p>
          <p v-else>Out of Stock</p>
          <p> {{ onSale }} </p>
          <p> Shipping: {{ shipping }}</p>
          <ProductDetails
            :details="socks.details"
          />
          <div
            v-for="(variant, index) in socks.variants"
            :key="variant.id"
            @mouseover="updateVariant(index)"
            class="color-circle"
            :style="{ backgroundColor: variant.color }"
          >
          </div>
          <button
            class="button"
            :class="{ disabledButton: !inStock }"
            :disabled="!inStock"
            @click="addToCart"
            >
              Add to Cart
          </button>
          <button
            class="button"
            @click="reset"
            >
              Erase Cart
          </button>
        </div>
      </div>
    </div>
</template>

<script setup lang="ts">
import { ref, computed } from 'vue';
import ProductDetails from './ProductDetails.vue'

const props = defineProps({
  cart: {
    type: Number,
    required: true
  },
  premium: {
    type: Boolean,
    required: true
  }
})

const product = ref('Socks')
const socks = ref({
    selectedVariant: 0,
    brand: 'Vue Mastery',
    details: ['50% cotton', '30% wool', '20% polyester'],
    variants: [
              { id: 2234, color: 'green', image: "./src//components//images//socks_green.png", quantity: 50, onSale: true},
              { id: 2235, color: 'blue', image: "./src//components//images//socks_blue.png",  quantity: 0, onSale: false},
              ],
    sizes: ['XS', 'S', 'L', 'XL']    
  })
  const title = computed(() => `${socks.value.brand} ${product.value}`)
  const image = computed(() => socks.value.variants[socks.value.selectedVariant].image)
  const inStock = computed(() => socks.value.variants[socks.value.selectedVariant].quantity)
  const onSale = computed(() => socks.value.variants[socks.value.selectedVariant].onSale ? `${socks.value.brand} ${product.value} is on sale` : '')
  const shipping = computed(() => props.premium ? `Free` : `5$`)


const addToCart = () => {
  props.cart ++
}

const updateVariant = (index: number) => {
  socks.value.selectedVariant = index
}

const reset = () => {
  props.cart = 0
}

</script>

<style lang="scss">

</style>