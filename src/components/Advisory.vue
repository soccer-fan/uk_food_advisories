<script setup>
defineProps({
  date: {
    type: Date,
    required: true
  },
  product: {
    type: String,
    required: true
  },
  riskStatement: {
    type: String,
    required: true
  }
})
</script>

<template>
    <div class="advisory">
        <h1>{{product}}</h1>
        <p>{{riskStatement}}</p>
    </div>
</template>
