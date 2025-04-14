<script setup>
import { ref } from 'vue'
let isAdded = ref(false)
let isLiked = ref(false)

function onClickAdd() {
  isAdded.value = !isAdded.value
}
function onLikeAdd() {
  isLiked.value = !isLiked.value
}
defineProps({
  imageUrl: String,
  albumName: String,
  releaseDate: Number,
  condition: String,
  vinylPrice: Number,
  /*   isLiked: Boolean,
  isAdded: Boolean,
  onClickAdd: Function,
  onClickLike: Function, */
})
</script>

<template>
  <div
    class="relative m-10 border border-slate-300 rounded-3xl p-8 cursor-pointer hover:-translate-y-2 hover:shadow-xl transition"
  >
    <img
      @click="onLikeAdd"
      class="absolute top-10 left-10"
      :src="!isLiked ? '/like-1.svg' : '/like-2.svg'"
      alt="Unclicked like button"
    />
    <img class="w-3xs" :src="imageUrl" alt="Vinyl disc picture" />

    <div class="mt-5">
      <p class="mb-5 h-12">{{ albumName }}</p>
      <div>
        <p>{{ releaseDate }}</p>
        <p>{{ condition }}</p>
      </div>
    </div>

    <div class="flex justify-between mt-5">
      <div class="flex flex-col">
        <span><b>Цена:</b></span>
        <span class="text-slate-400">{{ vinylPrice }} ₽</span>
      </div>
      <img @click="onClickAdd" :src="!isAdded ? '/plus.svg' : '/checked.svg'" alt="Add" />
    </div>
  </div>
</template>
