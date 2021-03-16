<template>
  <div class="flex justify-center items-center h-full w-full">
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 w-full">
      <div class="max-w-xl mx-auto">
        <Calculator />
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import Calculator from "./components/Calculator.vue";

export default defineComponent({
  name: "App",
  components: {
    Calculator,
  },
});
</script>
