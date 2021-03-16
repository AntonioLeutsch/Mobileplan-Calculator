<template>
  <div class="mt-1 relative shadow-sm">
    <div
      v-if="showEuro"
      class="absolute inset-y-0 left-0 pl-3 flex items-center pointer-events-none"
    >
      <div class="text-gray-500 sm:text-sm sm:leading-5">€</div>
    </div>

    <currency-input
      :id="id"
      :modelValue="modelValue"
      @update:modelValue="changeMoneyValue"
      required
      :class="[showEuro ? 'pl-7' : 'pl-3']"
      class="pr-12 sm:text-sm sm:leading-5 mt-1 block w-full border-gray-300 shadow-sm focus:border-green-300 focus:ring focus:ring-green-200 focus:ring-opacity-50"
    />
    <div
      class="absolute inset-y-0 right-0 pr-3 flex items-center pointer-events-nmonthly"
    >
      <div class="text-gray-500 sm:text-sm sm:leading-5">EUR</div>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import CurrencyInput from "./CurrencyInput.vue";

export default defineComponent({
  props: {
    modelValue: Number,
    id: String,
    showEuro: {
      type: Boolean,
      default: false,
    },
  },
  components: {
    CurrencyInput,
  },
  emits: ["update:modelValue"],
  methods: {
    changeMoneyValue(money: number) {
      this.$emit("update:modelValue", money); // previously was `this.$emit('input', title)`
    },
  },
});
</script>

