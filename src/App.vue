<script setup>

import AdvisoriesPanelWrapper from './components/AdvisoriesPanelWrapper.vue';
import SearchBar from './components/SearchBar.vue';
import {ref} from 'vue'

const currentSearchTerm = ref("")

const searchActivated = (searchTerm) => {
  currentSearchTerm.value = searchTerm;
}

const searchCleared = () => {
  currentSearchTerm.value = "";
}
</script>

<template>
  <header>
    <h1>UK Food Advisories</h1>
  </header>

  <main>
    <p>Check out the latest UK food advisories below or search for a particular type of food.</p>
    <SearchBar @searchActivated="searchActivated" @searchCleared="searchCleared"/>
    <AdvisoriesPanelWrapper :searchTerm="currentSearchTerm"/>
  </main>
</template>

<style>
@import './assets/base.css';

#app {
  max-width: 1280px;
  margin: 0 auto;
  padding: 2rem;

  font-weight: normal;
}

header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

a,
.green {
  text-decoration: none;
  color: hsla(160, 100%, 37%, 1);
  transition: 0.4s;
}

@media (hover: hover) {
  a:hover {
    background-color: hsla(160, 100%, 37%, 0.2);
  }
}

@media (min-width: 1024px) {
  body {
    display: flex;
    place-items: center;
  }

  #app {
    display: inline;
    
    padding: 0 2rem;
  }

  header {
    display: inline;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }
}
</style>
