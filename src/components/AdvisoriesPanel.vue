<!--
   This component has the list of advisories to display passed in and is responsible for the display logic of 
   showing them all
   -->

<script setup>
import Advisory from './Advisory.vue'
import {ref} from 'vue'

const pageNumber = ref(1)
const itemsPerPage = 5
const maxPages = 10

defineProps({
  items: {
    type: Array,
    required: true
  }
})

const getProductsDisplayName = (productDetails) => {
  return productDetails.map(entry => entry.productName).join(", ")
} 

const getItemsForCurrentPage = (items) => {
  // -1 to offset that we number pages from 1 but arrays index from 0
  return items.slice((pageNumber.value - 1) * itemsPerPage, pageNumber.value * itemsPerPage)
}

</script>

<template>
<div>
  <div style="min-height: 100vh;" v-if="items.length > 0">
    <div class="q-pa-lg">
      <div  class="advisories-panel-inner">
      <template v-for="item in getItemsForCurrentPage(items)" :key="item['@id']">
        <Advisory :date="item.created" :product="getProductsDisplayName(item.productDetails)" :riskStatement="item.problem[0].riskStatement"/>
      </template>
    </div>
      <q-pagination
      v-model="pageNumber"
      :max="items.length > maxPages ? maxPages : items.length"
      ></q-pagination>
    </div>
  </div>
  <h2 v-else>No results found</h2>
  </div>
  
  
</template>

<style scoped>
q-pagination {
  display: inline
}

.advisories-panel-inner {
  border:gray 1px solid;
  padding: 5px;
  margin-bottom: 5px;
}

</style>