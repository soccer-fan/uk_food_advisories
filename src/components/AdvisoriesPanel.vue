<script setup>
import Advisory from './Advisory.vue'
defineProps({
  items: {
    type: Array,
    required: true
  }
})

const getProductsDisplayName = (productDetails) => {
  return productDetails.map(entry => entry.productName).join(", ")
}
</script>

<template>
    <template v-for="item in items" :key="item['@id']">
        <Advisory :date="item.created" :product="getProductsDisplayName(item.productDetails)" :riskStatement="item.problem[0].riskStatement"/>
    </template>
</template>