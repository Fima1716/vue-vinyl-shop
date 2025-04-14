<script setup>
import VinylCard from './VinylCard.vue'
import { ref } from 'vue'
let isAdded = ref(false)
let isLiked = ref(false)
function onClickAdd() {
  isAdded.value = !isAdded.value
}
function onLikeAdd() {
  isLiked.value = !isLiked.value
}
</script>

<template>
  <div class="grid grid-cols-3 gap-5">
    <VinylCard
      image-url="/vinyl/vinyl1.jpg"
      album-name="Post Malone - Tribute To Nirvana"
      release-date="2025"
      condition="EX+/EX+"
      :vinyl-price="2000"
      :is-added="isAdded"
      :is-liked="isLiked"
      :onClickAdd="onClickAdd"
      :onClickLike="onLikeAdd"
    />
    <VinylCard
      image-url="/vinyl/vinyl2.jpg"
      album-name="Various, Andrew Lloyd Webber & Tim Rice* – Jesus Christ Superstar"
      release-date="1970"
      condition="M/M"
      vinyl-price="2000"
    />
    <VinylCard />
    <VinylCard />
    <VinylCard />
  </div>
</template>
