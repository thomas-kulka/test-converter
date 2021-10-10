<template>
  <div>
    <label>Amount of money:</label>
    <input
      class="input__wrapper mb-8 w-40"
      type="number"
      v-model="amount"
      @change="$emit('amountChange', amount)"
    />
  </div>
</template>

<script>
import { defineComponent, ref } from "@vue/composition-api";

export default defineComponent({
  setup() {
    const amount = ref(0);

    return { amount };
  }
});
</script>

<style lang="postcss" scoped>
.input__wrapper {
  @apply border-0 border-b border-gray-600 p-2;
}
</style>
