<script setup>
import Advisory from './Advisory.vue';
import AdvisoriesPanel from './AdvisoriesPanel.vue';
import { onMounted, ref } from 'vue';
const details = ref([])

const loadDetails = () => {
    fetch("https://data.food.gov.uk/food-alerts/id?_limit=1000")
    .then(jsonData => {
        jsonData.json()
        .then(data => {
            console.log(data)
            details.value = data.items
        })
    })
}

onMounted(() => {
    loadDetails()
})
</script>

<template>
    <AdvisoriesPanel v-if="details.length != 0" :items="details"/>
    <h1 v-else>Loading...</h1>
</template>
