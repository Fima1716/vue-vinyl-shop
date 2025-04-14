<script setup>
import VinylHeader from './components/VinylHeader.vue'
import VinylList from './components/VinylList.vue'
import VinylDrawer from './components/VinylDrawer.vue'
import { ref } from 'vue'
const isDrawerOpen = ref(false)
</script>

<template>
  <VinylDrawer :is-open="isDrawerOpen" @close="isDrawerOpen = false" />
  <div class="bg-white w-4/5 m-auto rounded-xl shadow-xl mt-12">
    <VinylHeader />
    <div class="flex justify-between items-center mr-20">
      <h2 class="text-3xl font-bold mb-8 mt-8 ml-12">Каталог пластинок</h2>

      <div class="flex gap-5">
        <select class="py-2 px-3 border rounded-md outline-none">
          <option>По названию</option>
          <option>Дешевле</option>
          <option>Дороже</option>
        </select>
        <div class="relative">
          <img class="absolute left-3 top-3" src="/search.svg" alt="Search icon" />
          <input
            class="border rounded-md py-2 pl-11 pr-4 outline-none focus:border-gray-400"
            placeholder="Поиск..."
            type="text"
          />
        </div>
      </div>
    </div>
    <VinylList />
  </div>
</template>
