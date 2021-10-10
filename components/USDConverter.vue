<template>
  <div>
    <Amount @amountChange="amountChange"></Amount>
    Main currency: USD (free api restriction)
    <br />
    to
    <CurrencySelector
      title="Output currency"
      @currencySelected="currencySelected"
    ></CurrencySelector>

    <CtaButton @input="count" cta="Count"></CtaButton>
    <span class="block mt-4">outcome: {{ outcome }}</span>
  </div>
</template>

<script>
import { defineComponent, ref } from "@vue/composition-api";
import axios from "axios";

export default defineComponent({
  setup() {
    const amount = ref(0);
    const conversion = ref();
    const outcome = ref();

    async function getCurrencies(currency, value) {
      try {
        const { data } = await axios.get(
          `http://api.currencylayer.com/live?access_key=5203be45b540d5b362a46f0e4fa7e7fa&currencies=${currency}`
        );

        conversion.value = data.quotes[Object.keys(data.quotes)];
      } catch (error) {
        console.log(error);
      }
    }

    function amountChange(value) {
      amount.value = value;
    }

    function currencySelected(value) {
      getCurrencies(value);
    }

    function count() {
      outcome.value =
        amount.value && conversion.value ? amount.value * conversion.value : 0;

      outcome.value = Math.round(outcome.value * 100) / 100;
    }

    return { amount, amountChange, count, currencySelected, outcome };
  }
});
</script>
