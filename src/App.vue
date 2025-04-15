<script lang="ts">
import {
  defineComponent,
  onUnmounted,
  onMounted,
  provide,
  ref,
  watch,
  reactive,
} from "vue";
import VinylHeader from "./components/VinylHeader.vue";
import VinylList from "./components/VinylList.vue";
import VinylDrawer from "./components/VinylDrawer.vue";

interface VinylItem {
  id: number;
  name: string;
  price: number;
  condition: string;
  year: number;
  imageUrl: string;
}

interface Filters {
  sortBy: string;
  searchQuery: string;
}

export default defineComponent({
  name: "App",
  components: {
    VinylHeader,
    VinylList,
    VinylDrawer,
  },
  setup() {
    const isDrawerOpen = ref(false);
    const fetchVinylData = ref<VinylItem[]>([]);

    const filters = reactive<Filters>({
      sortBy: "",
      searchQuery: "",
    });

    const fetchDataFoo = async (): Promise<void> => {
      try {
        const queryParams = new URLSearchParams();
        if (filters.sortBy) queryParams.append("sortBy", filters.sortBy);
        if (filters.searchQuery)
          queryParams.append("name", `*${filters.searchQuery}*`);

        const res = await fetch(
          `https://18d85f8cd41400df.mokky.dev/vinyl?${queryParams.toString()}`
        );
        const data = await res.json();
        console.log("Фильтры при fetch:", filters);
        console.log("Данные с сервера:", data);
        fetchVinylData.value = data;
      } catch (error) {
        console.error("Ошибка при загрузке данных:", error);
      }
    };

    const closeDrawer = () => {
      isDrawerOpen.value = false;
    };

    const openDrawer = () => {
      isDrawerOpen.value = true;
    };

    const handleKeydown = (e: KeyboardEvent) => {
      if (e.key === "Escape") {
        closeDrawer();
      }
    };

    const onChangeSelect = (e: Event) => {
      const target = e.target as HTMLSelectElement;
      filters.sortBy = target.value;
    };

    onMounted(() => {
      fetchDataFoo();
      window.addEventListener("keydown", handleKeydown);
    });

    onUnmounted(() => {
      window.removeEventListener("keydown", handleKeydown);
    });

    watch(filters, fetchDataFoo, { deep: true });

    provide("cartActions", { closeDrawer, openDrawer });

    return {
      isDrawerOpen,
      fetchVinylData,
      filters,
      onChangeSelect,
      openDrawer,
    };
  },
});
</script>

<template>
  <VinylDrawer v-if="isDrawerOpen" />
  <div class="bg-white w-4/5 m-auto rounded-xl shadow-xl mt-12">
    <VinylHeader @open-drawer="openDrawer" />
    <div class="flex justify-between items-center mr-20">
      <h2 class="text-3xl font-bold mb-8 mt-8 ml-12">Каталог пластинок</h2>

      <div class="flex gap-5">
        <select
          @change="onChangeSelect"
          class="py-2 px-3 border rounded-md outline-none"
        >
          <option value="name">По названию</option>
          <option value="price">Дешевле</option>
          <option value="-price">Дороже</option>
        </select>
        <div class="relative">
          <img
            class="absolute left-3 top-3"
            src="/search.svg"
            alt="Search icon"
          />
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
