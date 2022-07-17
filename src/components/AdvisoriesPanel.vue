<script setup>
import Advisory from './Advisory.vue'
defineProps({
  items: {
    type: Array,
    required: true
  }
})
</script>

<template>
    <template v-for="item in items" :key="item['@id']">
        <Advisory :date="item.created" product="item.productDetails[0]" :riskStatement="item.problem[0].riskStatement"/>
    </template>
</template>