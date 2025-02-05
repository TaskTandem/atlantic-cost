<script setup>
//vue
import { ref, onMounted } from 'vue';
//vue-router
import { RouterLink } from 'vue-router'
//components
import CardContainer from '@/components/CardContainer.vue';
//store
import { useProductStore, useAdminStore } from '@/stores'
const $P = useProductStore()
const { logged } = useAdminStore()

const products = ref(null)
const error = ref(false)

onMounted(async () => {
  const res = await $P.getProducts()
  if(res) products.value = res
  else error.value = true
})
</script>

<template>
  <div class="home-container">
    <div v-if="logged" class="admin-buttons">
      <RouterLink to="/categories" class="button">
        <span>Categorias</span>
      </RouterLink>
      <RouterLink to="/add/new" class="button">
        <span>Agregar producto</span>
      </RouterLink>
    </div>
    <div v-if="!products && !error" class="loading"><fa icon="spinner" /></div>
    <div v-else-if="!products && error" class="error">
      <p>Hubo un error al cargar los productos. Intentelo mas tarde.</p>
    </div>
    <CardContainer v-else :data="products" />
  </div>
</template>
