<script setup>
import Advisory from './Advisory.vue';
import AdvisoriesPanel from './AdvisoriesPanel.vue';
import { onMounted, watch, ref } from 'vue';

const props = defineProps({
  searchTerm: {
    type: String,
    required: true
  }
})

const details = ref([])
const isLoading = ref(true)

const loadDetails = (searchTerm) => {
    isLoading.value = true
    const queryParams = props.searchTerm != "" ? `search=${props.searchTerm}&` : ""
    fetch(`https://data.food.gov.uk/food-alerts/id?${queryParams}_limit=200&_sort=-created`)
    .then(jsonData => {
        jsonData.json()
        .then(data => {
            const validData = data.items.filter(item => item.productDetails && item.productDetails.length > 0)
            details.value = validData
            isLoading.value = false
        })
        // Filter so that we only get items with products and we merge the titles of those products
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
