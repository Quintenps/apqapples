<template>
  <div>
    <div class="flex flex-row gap-x-4">
      <number-input name="round1" :amount="apples[0]" />
      <number-input name="round2" :amount="apples[1]" />
      <number-input name="round3" :amount="apples[2]" />
      <number-input name="round4" :amount="apples[3]" />
    </div>
    <Button class="my-2" text="Submit run" v-on:click="addRun()" />
  </div>
</template>
<script>
import NumberInput from "./NumberInput.vue";
import Button from "./Button.vue";
export default {
  components: {
    Button,
    NumberInput,
  },
  data: function () {
    return {
      apples: [0, 0, 0, 0],
    };
  },
  methods: {
    addRun: function () {
      console.log(this.apples);
    },
  },
};
</script>
