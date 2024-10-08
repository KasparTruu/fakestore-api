<script setup>
import axios from 'axios';
import { onMounted, ref } from 'vue';

const products = ref([]);

const fetchAllProducts = async () => {
  const response = await axios.get('https://fakestoreapi.com/products');
  products.value = response.data;
}

onMounted(async () => await fetchAllProducts());
</script>

<template>
  <div class="bg-slate-500 py-10 text-white">
    <h1 class="text-center font-bold text-3xl">Welcome to the Fake Store</h1>
  </div>

  <div class="container mx-auto p-4">
    <div class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4 gap-6">
      <article 
        v-for="product in products" 
        :key="product.id" 
        class="bg-white rounded-lg shadow-lg overflow-hidden transition-transform duration-200 hover:scale-105 flex flex-col"
      >
        <img 
          class="w-full h-48 object-cover" 
          :src="product.image" 
          alt="Product image"
        >
        <div class="p-4 flex-1 flex flex-col justify-between">
          <h4 class="text-lg font-semibold text-gray-800 truncate">{{ product.title }}</h4>
          <p class="text-gray-600 mt-2">${{ product.price.toFixed(2) }}</p>
          <button class="mt-4 bg-blue-500 text-white py-2 rounded hover:bg-blue-600 transition">
            Add to Cart
          </button>
        </div>
      </article>
    </div>
  </div>
</template>

<style scoped>
h1 {
  font-size: 2rem;
}
</style>
