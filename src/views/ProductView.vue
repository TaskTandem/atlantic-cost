<script setup>
//vue
import { ref, onMounted } from "vue";
//store
import { useProductStore } from "../stores/product";
const { getProductById } = useProductStore()
//router
import { useRoute, useRouter } from "vue-router";
const route = useRoute()
const router = useRouter()
//product
const product = ref(null)
const error = ref(false)

onMounted(async () => {
  const res = await getProductById(route.params.id)
  if(res) product.value = res
  else error.value = true
})

</script>

<template>
  <div class="product-container">
    <div v-if="!product && !error" class="loading"><fa icon="spinner" /></div>

    <div v-else-if="!product && error" class="error">
      <p>No existe el producto que estas buscando</p>
      <button @click="router.push('/')">Volver al inicio</button>
    </div>

    <template v-else>
      <img :src="product.images[0]">

      <h1>{{ product.name }}</h1>
    </template>
  </div>
</template>