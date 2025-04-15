<script lang="ts">
import { defineComponent } from "vue";
import VinylCartItem from "./VinylCartItem.vue";

export default defineComponent({
  name: "VinylCartListItem",
  components: {
    VinylCartItem,
  },
});
</script>

<template>
  <div class="flex flex-col gap-1">
    <VinylCartItem />
    <VinylCartItem />
  </div>
</template>
