<script setup>
import VinylHeader from './components/icons/VinylHeader.vue'
import VinylList from './components/VinylList.vue'
</script>

<template>
  <div class="bg-white w-4/5 m-auto rounded-xl shadow-xl mt-12">
    <VinylHeader />
    <h2 class="text-3xl font-bold mb-8 mt-8 ml-12">Каталог пластинок</h2>
    <VinylList />
  </div>
</template>
