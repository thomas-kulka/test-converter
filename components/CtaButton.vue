<template>
  <button type="button" @click="$emit('input')">{{ cta }}</button>
</template>

<script>
import { defineComponent } from "@vue/composition-api";

export default defineComponent({
  props: {
    cta: {
      type: String,
      default: "Save"
    }
  }
});
</script>

<style lang="postcss" scoped>
button {
  @apply bg-blue-500 hover:bg-blue-700 text-white font-bold py-1 px-4 rounded block mt-4;
}
</style>
