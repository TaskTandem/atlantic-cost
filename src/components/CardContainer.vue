<script setup>
//components
import Card from './Card.vue';
//props
defineProps(['data'])
</script>

<template>
  <div class="cards-container">
    <Card v-for="(product, index) in data" :data="product" :key="index" />
  </div>
</template>