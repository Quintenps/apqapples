<template>
  <div>
    <div class="flex flex-col">
      <div class="grid grid-cols-4 gap-4 mb-4">
        <input
          type="number"
          class="px-4 text-gray-700 border border-solid border-gray-300 rounded focus:text-gray-700 focus:bg-white focus:border-blue-600 focus:outline-none"
          name="round1"
          v-model="run.apples[0]"
        />
        <input
          type="number"
          class="px-4 text-base font-normal text-gray-700 bg-white bg-clip-padding border border-solid border-gray-300 rounded transition ease-in-out m-0 focus:text-gray-700 focus:bg-white focus:border-blue-600 focus:outline-none"
          name="round2"
          v-model="run.apples[1]"
        />
        <input
          type="number"
          class="px-4 py-1.5 text-base font-normal text-gray-700 bg-white bg-clip-padding border border-solid border-gray-300 rounded transition ease-in-out m-0 focus:text-gray-700 focus:bg-white focus:border-blue-600 focus:outline-none"
          name="round3"
          v-model="run.apples[2]"
        />
        <input
          type="number"
          class="px-4 py-1.5 text-base font-normal text-gray-700 bg-white border border-solid border-gray-300 rounded transition ease-in-out m-0 focus:text-gray-700 focus:bg-white focus:border-blue-600 focus:outline-none"
          name="round4"
          v-model="run.apples[3]"
        />
      </div>
      <div>
        <Button text="Submit run" class="w-full" v-on:click="countApples()" />
      </div>
    </div>
  </div>
</template>
<script>
import Button from "./Button.vue";
export default {
  components: {
    Button,
  },
  props: {
    countApples: {
      type: Function,
    },
    run: {
      type: Object,
    },
  },
};
</script>
