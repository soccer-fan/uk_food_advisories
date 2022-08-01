<script setup>
import {ref} from 'vue'

const emit = defineEmits(['searchActivated', 'searchCleared'])

const searchTerm = ref("")

const clearSearchTermFromUI = () => {
    alert('etst')
    emit('searchCleared')
    searchTerm.value = "";
}

</script>

<template>
    <input v-model="searchTerm" placeholder="Enter search term here" />
    <button @click="$emit('searchActivated', searchTerm)">Search!</button>
    <button @click="clearSearchTermFromUI">Clear search term</button>
</template>
