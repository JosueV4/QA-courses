<script setup lang="ts">
import { ref, onMounted } from 'vue';
import { fetchProducts } from '@/api/products';

// Define la variable products como un ref reactivo
const products = ref([]);

// Usa onMounted para llamar a fetchProducts cuando el componente se monte
onMounted(async () => {
  try {
    const response = await fetchProducts();
    products.value = response;
    console.log('Productos:', products.value);
  } catch (error) {
    console.error("Error al obtener los productos:", error);
  }
});
</script>

<template>
  <div>
    <div v-if="products.length === 0">Cargando productos...</div>
    <div v-else>
      <ul>
        <li v-for="product in products" :key="product.id">
          {{ product.title }} - ${{ product.price }}
        </li>
      </ul>
    </div>
  </div>
</template>