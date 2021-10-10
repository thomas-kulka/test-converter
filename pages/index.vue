<template>
  <div class="page">
    <USDConverter></USDConverter>

    <hr class="border-gray-600 my-4" />

    <PLNConverter></PLNConverter>
  </div>
</template>

<script>
import { defineComponent } from "@vue/composition-api";

export default defineComponent({
  setup() {}
});
</script>

<style lang="postcss" scoped>
.page {
  @apply px-4 py-12;
}
</style>
