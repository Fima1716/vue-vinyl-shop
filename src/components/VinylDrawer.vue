<script setup>
import VinylDrawerHead from './VinylDrawerHead.vue'
import VinylCartListItem from './VinylCartListItem.vue'
import { inject } from 'vue'
const { closeDrawer } = inject('cartActions')
</script>

<template>
  <div
    @keydown="escape"
    @click="closeDrawer"
    class="fixed top-0 left-0 h-full w-full bg-black z-10 opacity-50"
  ></div>
  <div class="fixed top-0 right-0 bg-white w-96 h-full bg-white z-11 p-8 overflow-auto">
    <VinylDrawerHead />
    <VinylCartListItem />

    <div>
      <div class="flex flex-col gap-2 mt-5">
        <div class="flex gap-2">
          <span>Итого:</span>
          <div class="flex-1 border-b border-dashed"></div>
          <b>2500 ₽</b>
        </div>
        <button
          disabled=""
          class="transition bg-blue-500 w-full rounded-xl mt-10 py-3 cursor-pointer hover:bg-blue-600 active:bg-blue-700 disabled:bg-slate-300"
        >
          Оформить заказ
        </button>
      </div>
    </div>
  </div>
</template>
