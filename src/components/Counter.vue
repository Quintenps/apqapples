<template>
  <div>
    <div v-if="startRun">
      <div class="flex flex-row gap-x-4">
        <number-input name="round1" />
        <number-input name="round2" />
        <number-input name="round3" />
        <number-input name="round4" />
      </div>
      <Button class="my-2" text="Submit run" v-on:click="startRun = false" />
    </div>
    <div v-else>
      <Button class="my-2" text="Start run" v-on:click="startRun = true" />
    </div>
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
      startRun: false,
      apples: [0, 0, 0, 0],
    };
  },
};
</script>
