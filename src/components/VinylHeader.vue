<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  name: "VinylHeader",
  emits: ["openDrawer"],
  setup(_, { emit }) {
    const handleOpenDrawer = () => {
      emit("openDrawer");
    };

    return {
      handleOpenDrawer,
    };
  },
});
</script>

<template>
  <header class="flex justify-between border-b border-slate-300 px-10 py-4">
    <div class="flex items-center gap-3">
      <img class="w-30" src="/logo.svg" alt="Logo" />
      <div>
        <h2 class="text-xl font-bold uppercase">Fima Vinyl Store</h2>
        <p class="text-slate-500 lowercase">Магазин виниловых пластинок</p>
      </div>
    </div>

    <ul class="flex items-center gap-10">
      <li
        @click="handleOpenDrawer"
        class="flex items-center gap-1 text-gray-500 hover:text-black cursor-pointer"
      >
        <img src="/cart.svg" alt="Cart" /><b>Корзина</b>
      </li>
    </ul>
  </header>
</template>
