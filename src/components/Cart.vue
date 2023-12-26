<template>

    <div class="nav-bar"></div>

    <div class="cart">Cart({{ socks.cart }})</div>
    
    <div class="product-display">
      <div class="product-container">
        <div class="product-image">
          <img :src="socks.img">
        </div>
        <div class="product-info">
          <h1>{{ product }}</h1>
          <p v-if="socks.inventory >= 10">In Stock</p>
          <p v-else-if="socks.inventory < 10 && socks.inventory > 0">Almost sold out</p>
          <p v-else>Out of Stock</p>
          <ul>
            <li
              v-for="(detail, index) in socks.details"
              :key="index"
            >
              {{ `${index + 1}. ${detail}` }}
            </li> 
          </ul>
          <div
            v-for="(variant, index) in socks.variants"
            :key="variant.id"
            @mouseover="updateVariant(variant.image)"
          >
            {{ variant.color }}
          </div>
          <button
            class="button"
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
import { ref } from 'vue';


const product = ref('Shoes')
const socks = ref({
    cart: 0,
    img: "./src//components//images//socks_green.png",
    inventory: 10,
    onSale: true,
    details: ['50% cotton', '30% wool', '20% polyester'],
    variants: [
              { id: 2234, color: 'green', image: "./src//components//images//socks_green.png", },
              { id: 2235, color: 'blue', image: "./src//components//images//socks_blue.png", },
              ],
    sizes: ['XS', 'S', 'L', 'XL']    
  })
const url = 'https://www.vuemastery.com/'

const addToCart = () => {
  socks.value.cart ++
}

const updateVariant = (variantImage: string) => {
  socks.value.img = variantImage
}

const reset = () => {
  socks.value.cart = 0
}


</script>

<style lang="scss">

body {
  background-color: #f2f2f2;
  margin: 0px;
  font-family: tahoma;
  color: #282828;
}

.button {
  margin: 30px;
  background-color: #39495c;
  border-radius: 5px;
  font-size: 18px;
  width: 160px;
  height: 60px;
  color: white;
  padding: 20px;
  box-shadow: inset 0 -0.6em 1em -0.35em rgba(0, 0, 0, 0.17),
    inset 0 0.6em 2em -0.3em rgba(255, 255, 255, 0.15),
    inset 0 0 0em 0.05em rgba(255, 255, 255, 0.12);
  text-align: center;
  cursor: pointer;
}

.cart {
  margin: 25px 100px;
  float: right;
  border: 1px solid #d8d8d8;
  padding: 10px 30px;
  background-color: white;
  -webkit-box-shadow: 0px 2px 15px -12px rgba(0, 0, 0, 0.57);
  -moz-box-shadow: 0px 2px 15px -12px rgba(0, 0, 0, 0.57);
  box-shadow: 2px 15px -12px rgba(0, 0, 0, 0.57);
}

.color-circle {
  width: 50px;
  height: 50px;
  margin-top: 8px;
  border: 2px solid #d8d8d8;
  border-radius: 50%;
}


.disabledButton {
  background-color: #d8d8d8;
  cursor: not-allowed;
}

h1 {
  font-size: 50px;
}

h3 {
  font-size: 25px;
}

img {
  border: 2px solid #d8d8d8;
  width: 70%;
  margin: 40px;
  padding: 15px;
  -webkit-box-shadow: 0px 2px 15px -12px rgba(0, 0, 0, 0.57);
  -moz-box-shadow: 0px 2px 15px -12px rgba(0, 0, 0, 0.57);
  box-shadow: 2px 15px -12px rgba(0, 0, 0, 0.57);
}

input {
  width: 100%;
  height: 40px;
  margin-bottom: 20px;
}

label {
  font-size: 20px;
  margin-bottom: 5px;
}

li {
  font-size: 18px;
}

.nav-bar {
  background: linear-gradient(-90deg, #84cf6a, #16c0b0);
  height: 60px;
  margin-bottom: 25px;
  -webkit-box-shadow: 0px 2px 15px -12px rgba(0, 0, 0, 0.57);
  -moz-box-shadow: 0px 2px 15px -12px rgba(0, 0, 0, 0.57);
  box-shadow: 1px 1px 5px rgba(0, 0, 0, 0.57);
}

p {
  font-size: 22px;
}

.product-display {
  display: flex;
  flex-direction: column;
  padding: 1rem;
}

.product-container {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
}

.product-image,
.product-info {
  width: 50%;
}

.review-form {
  display: flex;
  flex-direction: column;
  width: 425px;
  padding: 20px;
  margin: 40px;
  border: 2px solid #d8d8d8;
  background-color: white;
  -webkit-box-shadow: 0px 2px 15px -12px rgba(0, 0, 0, 0.57);
  -moz-box-shadow: 0px 2px 15px -12px rgba(0, 0, 0, 0.57);
  box-shadow: 2px 15px -12px rgba(0, 0, 0, 0.57);
}

.review-container {
  width: 425px;
  padding: 20px;
  background-color: white;
  -webkit-box-shadow: 0px 2px 20px -12px rgba(0, 0, 0, 0.57);
  -moz-box-shadow: 0px 2px 20px -12px rgba(0, 0, 0, 0.57);
  box-shadow: 2px 20px -12px rgba(0, 0, 0, 0.57);
  margin-left: 40px;
  border: 2px solid #d8d8d8;
}

.review-container li {
  margin-bottom: 30px;
}

.review-form .button {
  display: block;
  margin: 30px auto;
}

select {
  height: 40px;
  font-size: 20px;
  background-color: white;
  cursor: pointer;
}

textarea {
  width: 95%;
  height: 70px;
  padding: 10px;
  font-size: 20px;
  margin-bottom: 20px;
}

ul {
  list-style-type: none;
}

@media only screen and (max-width: 600px) {
  .container {
    flex-direction: column;
  }

  .product-image,
  .product-info {
    margin-left: 10px;
    width: 100%;
  }

  .review-form {
    width: 90%;
  }
}

</style>