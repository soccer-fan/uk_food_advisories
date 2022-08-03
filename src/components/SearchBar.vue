<!-- 
    This component provides the search bar that allows users to search for particular types of food.
    Events from button presses either setting or clearing the search term are emitted up to the parent
    so that the AdvisoriesPanelWrapper can update with new information.
 -->

<script setup>
import {ref} from 'vue'

const emit = defineEmits(['searchActivated', 'searchCleared'])

// Used to track the current search term - linked to the text input field
const searchTerm = ref("")

const clearSearchTermFromUI = () => {
    // Notify parent and clear value to update the input field and make it blank
    emit('searchCleared')
    searchTerm.value = "";
}

</script>

<template>
<div class="searchbar-wrapper">

    <input outlined v-model="searchTerm" @keyup.enter="$emit('searchActivated', searchTerm)" placeholder="Enter search term here" />
    <q-btn color="positive" @click="$emit('searchActivated', searchTerm)">Search!</q-btn>
    <q-btn color="negative" @click="clearSearchTermFromUI">Clear search term</q-btn>

</div>
</template>

<style scoped>
button {
    margin: 5px;
}

input   {
    margin: 5px;
}

.searchbar-wrapper {
    background-color:gray;      
}
</style>
