<script lang="ts">
import VinylCard from "./VinylCard.vue";
import { defineComponent } from "vue";

/* interface VinylItem {
  id: number;
  name: string;
  price: number;
  condition: string;
  year: number;
  imageUrl: string;
} */

export default defineComponent({
  name: "VinylList",
  components: { VinylCard },
  props: {
    items: {
      type: Array,
      required: true,
    },
  },
});
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
    />
  </div>
</template>
