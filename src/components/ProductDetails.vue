<template>
    <ul>
      <li
        v-for="(detail, index) in details"
        :key="index"
      >
        {{ `${index + 1}. ${detail}` }}
      </li> 
    </ul>
</template>

<script setup lang="ts">

const props = defineProps({
  details: {
    type: Array,
    required: true
  }
})

</script>

<style lang="scss" scoped>

</style>