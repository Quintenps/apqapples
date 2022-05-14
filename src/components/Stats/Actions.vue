<template>
  <div>
    <h3 class="text-white font-bold uppercase tracking-tight mt-6 mb-2">
      Actions
    </h3>
    <div class="flex flex-wrap gap-2">
      <Button
        text="Current run stats to clipboard"
        v-on:click="calculateCurrentRunApples()"
      />
      <Button
        text="All time stats to clipboard"
        v-on:click="calculateTotalApples()"
      />
      <Button
        text="Reset stats"
        v-on:click="resetStats()"
        class="bg-red-500 hover:bg-red-700"
      />
    </div>
  </div>
  <transition name="actionMessage">
    <span v-show="actionMessage" class="text-white italic font-bold text-md">{{
      actionMessage
    }}</span>
  </transition>
</template>
<script>
import Button from "../Generic/Button.vue";

export default {
  components: { Button },
  props: {
    resetStats: {
      type: Function,
    },
    currentRun: {
      type: Object,
    },
    runs: {
      type: Array,
    },
  },
  data() {
    return {
      actionMessage: null,
    };
  },
  methods: {
    showMessage() {
      this.actionMessage = "Stats copied to clipboard!";
      setTimeout(() => (this.actionMessage = null), 1500);
    },
    calculateCurrentRunApples: function () {
      var message = `My current run: ${this.currentRun.apples[0]}, ${this.currentRun.apples[1]}, ${this.currentRun.apples[2]}, ${this.currentRun.apples[3]}`;
      this.copyTextToClipboard(message);
      this.showMessage();
    },
    calculateTotalApples: function () {
      var totalApples = this.runs
        .map((x) => x.apples)
        .flat()
        .reduce((total, cur) => total + cur, 0);
      var message = `I collected a total of ${totalApples} apples in ${this.runs.length} runs`;
      this.copyTextToClipboard(message);
      this.showMessage();
    },
    copyTextToClipboard(msg) {
      navigator.clipboard.writeText(msg).then(
        function () {
          console.log("Async: Copying to clipboard was successful!");
        },
        function (err) {
          console.error("Async: Could not copy text: ", err);
        }
      );
    },
  },
};
</script>
