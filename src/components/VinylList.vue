<script setup>
import VinylCard from './VinylCard.vue'
/* import { ref } from 'vue' */

defineProps({
  items: Array,
})
</script>

<template>
  <div class="grid grid-cols-3 gap-5">
    <VinylCard
      v-for="item in items"
      :key="item.id"
      :image-url="item.imageUrl"
      :album-name="item.name"
      :release-date="item.year"
      :condition="item.condition"
      :vinyl-price="item.price"
      :is-added="isAdded"
      :is-liked="isLiked"
      :onClickAdd="onClickAdd"
      :onClickLike="onLikeAdd"
    />
  </div>
</template>
