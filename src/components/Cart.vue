<template>
    <div>
        <h1> {{ product }} </h1>
        <p> {{ description }} </p>

    </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';


const product = ref('Shoes')
const description = ref('Blue')


</script>

<style lang="scss">

</style>