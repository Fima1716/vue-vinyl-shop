<script setup>
import VinylHeader from './components/VinylHeader.vue'
import VinylList from './components/VinylList.vue'
import VinylDrawer from './components/VinylDrawer.vue'
import { onUnmounted, onMounted, provide, ref, watch, reactive } from 'vue'
const isDrawerOpen = ref(false)

const fetchVinylData = ref([])
const filters = reactive({
  sortBy: '',
  searchQuery: '',
})
const fetchDataFoo = async () => {
  try {
    const queryParams = new URLSearchParams()
    if (filters.sortBy) queryParams.append('sortBy', filters.sortBy)
    if (filters.searchQuery) queryParams.append('name', `*${filters.searchQuery}*`)

    const res = await fetch(`https://18d85f8cd41400df.mokky.dev/vinyl?${queryParams.toString()}`)
    const data = await res.json()
    console.log(data)
    fetchVinylData.value = data
  } catch (error) {
    console.error('Ошибка при загрузке данных:', error)
  }
}

const closeDrawer = () => {
  isDrawerOpen.value = false
}
const openDrawer = () => {
  isDrawerOpen.value = true
}
onMounted(() => {
  fetchDataFoo()
  window.addEventListener('keydown', handleKeydown)
})

watch(filters, fetchDataFoo)

const onChangeSelect = (e) => {
  filters.sortBy = e.target.value
}
const handleKeydown = (e) => {
  if (e.key === 'Escape') {
    closeDrawer()
  }
}

onUnmounted(() => {
  window.removeEventListener('keydown', handleKeydown)
})
provide('cartActions', { closeDrawer, openDrawer })
</script>

<template>
  <VinylDrawer v-if="isDrawerOpen" />
  <div class="bg-white w-4/5 m-auto rounded-xl shadow-xl mt-12">
    <VinylHeader @open-drawer="openDrawer" />
    <div class="flex justify-between items-center mr-20">
      <h2 class="text-3xl font-bold mb-8 mt-8 ml-12">Каталог пластинок</h2>

      <div class="flex gap-5">
        <select @change="onChangeSelect" class="py-2 px-3 border rounded-md outline-none">
          <option value="name">По названию</option>
          <option value="price">Дешевле</option>
          <option value="-price">Дороже</option>
        </select>
        <div class="relative">
          <img class="absolute left-3 top-3" src="/search.svg" alt="Search icon" />
          <input
            v-model="filters.searchQuery"
            class="border rounded-md py-2 pl-11 pr-4 outline-none focus:border-gray-400"
            placeholder="Поиск..."
            type="text"
          />
        </div>
      </div>
    </div>
    <VinylList :items="fetchVinylData" />
  </div>
</template>
