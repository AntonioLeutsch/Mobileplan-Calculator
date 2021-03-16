<template>
  <form
    class="bg-white border-gray-200 border-2 overflow-hidden"
    @submit.prevent="calculate"
  >
    <div class="px-4 py-5 sm:p-6">
      <div>
        <label
          for="phone"
          class="block text-sm font-medium leading-5 text-gray-700"
        >
          Retail Phone Price
        </label>

        <money-input id="phone" v-model="calculation.phone" />
      </div>
      <div class="mt-6">
        <label
          for="onetime"
          class="block text-sm font-medium leading-5 text-gray-700"
        >
          One-Time Payment
        </label>

        <money-input id="onetime" v-model="calculation.onetime" />
      </div>
      <div class="sm:grid grid-cols-2 gap-6">
        <div class="mt-6">
          <label
            for="monthly_first"
            class="block text-sm font-medium leading-5 text-gray-700"
          >
            Monthly Rate First 12 Months
          </label>
          <money-input id="monthly_first" v-model="calculation.monthly_first" />
        </div>
        <div class="mt-6">
          <label
            for="monthly_second"
            class="block text-sm font-medium leading-5 text-gray-700"
          >
            Monthly Rate Last 12 Months
          </label>
          <money-input
            id="monthly_second"
            v-model="calculation.monthly_second"
          />
        </div>
      </div>
      <div
        v-if="calculation.total"
        class="bg-green-50 text-center p-4 text-green-900 mt-6 border-b-4 border-green-600"
      >
        monthly real price: {{ currencyFormatDE(calculation.total) }}
      </div>
    </div>
    <div class="bg-gray-100 px-4 py-4 sm:px-6">
      <button
        class="bg-green-500 rounded-none border-2 border-green-600 text-white p-3 w-full shadow font-bold"
        type="submit"
      >
        Calculate!
      </button>
    </div>
  </form>
</template>


<script lang="ts">
import { defineComponent, reactive } from "vue";
import MoneyInput from "./MoneyInput.vue";

interface Calculation {
  phone: number;
  onetime: number;
  monthly_first: number;
  monthly_second: number;
  total: number;
}

export default defineComponent({
  components: { MoneyInput },
  setup() {
    const calculation = reactive<Calculation>({
      phone: 0,
      onetime: 0,
      total: 0,
      monthly_first: 0,
      monthly_second: 0
    });

    return {
      calculation,
    };
  },
  methods: {
    calculate(): void {
      const {
        monthly_first,
        monthly_second,
        onetime,
        phone,
      } = this.calculation;

      this.calculation.total = this.round(
        (monthly_first * 12 + monthly_second * 12 + onetime - phone) / 24
      );
    },
    round(value: number): number {
      return Math.round((value + Number.EPSILON) * 100) / 100;
    },
    currencyFormatDE(value: number): string {
      return (
        value
          .toFixed(2) // always two decimal digits
          .replace(".", ",") // replace decimal point character with ,
          .replace(/(\d)(?=(\d{3})+(?!\d))/g, "$1.") + " €"
      );
    },
  },
});
</script>
