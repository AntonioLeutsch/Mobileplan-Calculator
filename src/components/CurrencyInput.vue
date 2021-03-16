<template>
  <input type="text" ref="inputRef" :value="formattedValue" placeholder="0,00" />
</template>

<script>
import useCurrencyInput from "vue-currency-input";

export default {
  name: "CurrencyInput",
  props: {
    modelValue: Number,
    options: Object,
  },
  setup(props) {

    const options = {
      currency: 'EUR',
      locale: 'de',
      allowNegative: false,
      precision: { min: 2, max: 2 },
      ...props.options
    }

    const { formattedValue, inputRef } = useCurrencyInput(options);

    return { inputRef, formattedValue };
  },
};
</script>
