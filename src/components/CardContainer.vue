<script setup>
//components
import Card from './Card.vue';
//store
import { useWindowStore } from '@/stores';
const $W = useWindowStore()
//props
defineProps(['data'])
</script>

<template>
  <div v-if="$W.width < 768" class="cards-container">
    <Card v-for="(product, index) in data" :data="product" :key="index" />
  </div>
  <div v-else class="cards-container">
    <Card v-for="(product, index) in data" :data="product" :key="index" />
  </div>
</template>