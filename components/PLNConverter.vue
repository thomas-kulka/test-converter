<template>
  <div>
    <Amount @amountChange="amountChange"></Amount>
    Main currency: PLN (free api restriction)
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
    const conversion = ref(0);
    const outcome = ref();

    async function getCurrencies(currency) {
      try {
        const { data } = await axios.get(
          `https://api.nbp.pl/api/exchangerates/tables/c/?format=json`
        );

        if (currency === "PLN") conversion.value = 1;
        else
          data[0].rates.forEach(rate => {
            if (currency === rate.code) conversion.value = rate.bid;
          });
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
