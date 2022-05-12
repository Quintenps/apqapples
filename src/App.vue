<template>
  <div id="main" class="container mx-auto px-4">
    <div class="flex flex-col">
      <div>
        <h1 class="text-2xl font-bold underline">APQ Apple Counter</h1>
      </div>
      <div>
        <div class="flex flex-col lg:flex-row">
          <div class="basis-full lg:basis-2/5">
            <Counter :countApples="countApples" :run="this.currentRun" />
          </div>
          <div class="basis-full lg:basis-3/5">
            <History
              class="place-content-center"
              :runs="this.runs"
              :delete-run="deleteRun"
            />
          </div>
        </div>
        <Button text="Copy stats" v-on:click="calculateStats()" />
        <Button text="Copy last run" />
      </div>
    </div>
  </div>
</template>
<script>
import Counter from "./components/Counter.vue";
import History from "./components/History.vue";
import Button from "./components/Button.vue";
export default {
  components: {
    Counter,
    History,
    Button,
  },
  data() {
    return {
      runs: [],
      currentRun: { index: 0, apples: [0, 0, 0, 0] },
    };
  },
  methods: {
    countApples: function () {
      var runs = localStorage.getItem("runs");
      if (runs == null) {
        console.log("No runs found yet!");
        runs = [this.currentRun];
      } else {
        runs = JSON.parse(runs);
        console.log(`Found existing ${runs.length} runs`);
        runs.push(this.currentRun);
      }

      localStorage.setItem("runs", JSON.stringify(runs));
      this.runs = runs;
      this.initiateNewRun();
    },
    calculateStats: function () {
      var totalApples = this.runs
        .map((x) => x.apples)
        .reduce((sum, cur) => sum + cur, 0);
      console.log(totalApples);
    },
    initiateNewRun: function () {
      var elements = this.runs.length;
      console.log(`Initiating testrun with index ${elements}`);
      if (elements == 0) {
        this.currentRun = { index: 0, apples: [0, 0, 0, 0] };
      } else if (elements == 1) {
        var lastItemIndex = this.runs[0].index;
        this.currentRun = { index: lastItemIndex + 1, apples: [0, 0, 0, 0] };
      } else {
        var lastItemIndex = this.runs[elements - 1].index;
        this.currentRun = { index: lastItemIndex + 1, apples: [0, 0, 0, 0] };
      }
    },
    deleteRun: function (index) {
      console.log(`Deleting item  ${index}`);
      const indexOfObject = this.runs.findIndex((run) => {
        return run.index == index;
      });
      console.log(indexOfObject);
      this.runs.splice(indexOfObject, 1);
      localStorage.setItem("runs", JSON.stringify(this.runs));
      this.initiateNewRun();
    },
  },
  mounted() {
    var runs = localStorage.getItem("runs");
    if (runs == null) {
      return;
    }

    this.runs = JSON.parse(runs);
    this.initiateNewRun();
  },
};
</script>
