<script lang="ts">
import { defineComponent } from "vue";
import type { PropType } from "vue";
import VinylCard from "./VinylCard.vue";

interface VinylItem {
  id: number;
  name: string;
  price: number;
  condition: string;
  year: number;
  imageUrl: string;
}

export default defineComponent({
  name: "VinylList",
  components: { VinylCard },
  props: {
    items: {
      type: Array as PropType<VinylItem[]>,
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
