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

const loadDetails = (searchTerm) => {
    details.value = []
    const queryParams = props.searchTerm != "" ? `search=${props.searchTerm}&` : ""
    fetch(`https://data.food.gov.uk/food-alerts/id?${queryParams}_limit=100&_sort=-created`)
    .then(jsonData => {
        jsonData.json()
        .then(data => {
            const validData = data.items.filter(item => item.productDetails && item.productDetails.length > 0)
            console.log(validData)
            details.value = validData
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
    <AdvisoriesPanel v-if="details.length != 0" :items="details"/>
    <h1 v-else>Loading...</h1>
</template>
