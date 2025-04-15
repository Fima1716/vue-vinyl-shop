<script lang="ts">
import { defineComponent, ref } from "vue";

export default defineComponent({
  name: "VinylCard",
  props: {
    imageUrl: { type: String, required: true },
    albumName: { type: String, required: true },
    releaseDate: { type: Number, required: true },
    condition: { type: String, required: true },
    vinylPrice: { type: Number, required: true },
  },
  setup(props) {
    const isAdded = ref(false);
    const isLiked = ref(false);

    const onClickAdd = () => {
      isAdded.value = !isAdded.value;
    };
    const onLikeAdd = () => {
      isLiked.value = !isLiked.value;
    };

    return {
      imageUrl: props.imageUrl,
      albumName: props.albumName,
      releaseDate: props.releaseDate,
      condition: props.condition,
      vinylPrice: props.vinylPrice,
      isAdded,
      isLiked,
      onClickAdd,
      onLikeAdd,
    };
  },
});
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
      <img
        @click="onClickAdd"
        :src="!isAdded ? '/plus.svg' : '/checked.svg'"
        alt="Add"
      />
    </div>
  </div>
</template>
