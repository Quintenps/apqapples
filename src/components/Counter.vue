<template>
  <div>
    <div class="flex flex-row gap-x-4">
      <input
        type="number"
        class="form-control block w-full px-3 py-1.5 text-base font-normal text-gray-700 bg-white bg-clip-padding border border-solid border-gray-300 rounded transition ease-in-out m-0 focus:text-gray-700 focus:bg-white focus:border-blue-600 focus:outline-none"
        name="round1"
        v-model="run.apples[0]"
      />
      <input
        type="number"
        class="form-control block w-full px-3 py-1.5 text-base font-normal text-gray-700 bg-white bg-clip-padding border border-solid border-gray-300 rounded transition ease-in-out m-0 focus:text-gray-700 focus:bg-white focus:border-blue-600 focus:outline-none"
        name="round2"
        v-model="run.apples[1]"
      />
      <input
        type="number"
        class="form-control block w-full px-3 py-1.5 text-base font-normal text-gray-700 bg-white bg-clip-padding border border-solid border-gray-300 rounded transition ease-in-out m-0 focus:text-gray-700 focus:bg-white focus:border-blue-600 focus:outline-none"
        name="round3"
        v-model="run.apples[2]"
      />
      <input
        type="number"
        class="form-control block w-full px-3 py-1.5 text-base font-normal text-gray-700 bg-white bg-clip-padding border border-solid border-gray-300 rounded transition ease-in-out m-0 focus:text-gray-700 focus:bg-white focus:border-blue-600 focus:outline-none"
        name="round4"
        v-model="run.apples[3]"
      />
    </div>
    <Button class="my-2" text="Submit run" v-on:click="countApples()" />
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
