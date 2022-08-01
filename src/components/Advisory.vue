<script setup>
defineProps({
  date: {
    type: String,
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
        <h4>{{date}}: {{product}}</h4>
        <p>{{riskStatement}}</p>
    </div>
</template>
