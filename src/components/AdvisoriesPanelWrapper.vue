<!-- 
    This wraps the advisories panel and is reponsible for fetching the raw data from the API,
    factoring in any current search term that has been set. This data is then passed into the 
    AdvisoriesPanel component, which handles the display logic
 -->

<script setup>
import AdvisoriesPanel from './AdvisoriesPanel.vue';
import { onMounted, watch, ref } from 'vue';

const props = defineProps({
  searchTerm: {
    type: String,
    required: true
  }
})

// Used to hold fetched advisory details from the API
const details = ref([])

// Used to track if we are currently fetching from API - if we are, we display loading message
const isLoading = ref(true)

const loadDetails = (searchTerm) => {
    isLoading.value = true
    const queryParams = props.searchTerm != "" ? `search=${props.searchTerm}&` : ""
    fetch(`https://data.food.gov.uk/food-alerts/id?${queryParams}_limit=200&_sort=-created`)
    .then(jsonData => {
        jsonData.json()
        .then(data => {
            // Filter so that we only get items with products and we merge the titles of those products
            const validData = data.items.filter(item => item.productDetails && item.productDetails.length > 0)
            details.value = validData
            isLoading.value = false
        })
    })
}

onMounted(() => {
    loadDetails()
})

watch(props, () => {
    loadDetails()
})

</script>

<template>
    <AdvisoriesPanel v-if="isLoading === false" :items="details"/>
    <h1 v-else>Loading...</h1>
</template>
