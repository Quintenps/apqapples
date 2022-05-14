<template>
  <div>
    <div class="flex flex-col">
      <h3 class="text-white font-bold uppercase tracking-tight mt-6 mb-2">
        Run counter
      </h3>
      <div class="grid grid-cols-4 gap-4 mb-4">
        <input
          type="number"
          min="0"
          max="15"
          class="px-4 py-1.5 text-gray-700 border border-solid border-gray-300 rounded focus:text-gray-700 focus:bg-white focus:border-blue-600 focus:outline-none"
          name="round1"
          v-model="run.apples[0]"
        />
        <input
          type="number"
          min="0"
          max="15"
          class="px-4 text-base font-normal text-gray-700 bg-white bg-clip-padding border border-solid border-gray-300 rounded transition ease-in-out m-0 focus:text-gray-700 focus:bg-white focus:border-blue-600 focus:outline-none"
          name="round2"
          v-model="run.apples[1]"
        />
        <input
          type="number"
          min="0"
          max="15"
          class="px-4 text-base font-normal text-gray-700 bg-white bg-clip-padding border border-solid border-gray-300 rounded transition ease-in-out m-0 focus:text-gray-700 focus:bg-white focus:border-blue-600 focus:outline-none"
          name="round3"
          v-model="run.apples[2]"
        />
        <input
          type="number"
          min="0"
          max="15"
          class="px-4 text-base font-normal text-gray-700 bg-white border border-solid border-gray-300 rounded transition ease-in-out m-0 focus:text-gray-700 focus:bg-white focus:border-blue-600 focus:outline-none"
          name="round4"
          v-model="run.apples[3]"
        />
      </div>
      <div>
        <Button
          text="Submit run"
          class="lg:w-full md:w-full disabled:bg-gray-600"
          :disabled="this.disabledState"
          v-on:click="countApples(), disableButton()"
        />
      </div>
    </div>
  </div>
</template>
<script>
import { TableBodyCell } from "@jobinsjp/vue3-datatable";
import Button from "./Generic/Button.vue";
export default {
  components: {
    Button,
    TableBodyCell,
  },
  props: {
    countApples: {
      type: Function,
    },
    run: {
      type: Object,
    },
  },
  data() {
    return {
      disabledState: false,
    };
  },
  methods: {
    disableButton: function () {
      console.log("Disabled!");
      this.disabledState = true;
      setTimeout(() => (this.disabledState = false), 1500);
    },
  },
};
</script>
