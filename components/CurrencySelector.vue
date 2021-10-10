<template>
  <div class="inline-block">
    <select
      name="currency"
      @change="currencySelection"
      class="border-0 border-b border-gray-600 w-40"
    >
      <option value=""></option>
      <option v-for="currency in currencies" :key="currency" :value="currency">
        {{ currency }}
      </option>
    </select>
  </div>
</template>

<script>
import { defineComponent } from "@nuxtjs/composition-api";

export default defineComponent({
  props: {
    title: {
      type: String,
      default: ""
    }
  },
  setup(_, { emit }) {
    const currencies = ["USD", "EUR", "PLN", "GBP"];

    function currencySelection(currency) {
      emit("currencySelected", currency.target.value);
    }

    return { currencies, currencySelection };
  }
});
</script>
