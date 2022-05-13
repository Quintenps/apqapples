<template>
  <div id="main" class="container mx-auto px-4">
    <div class="flex flex-col">
      <div>
        <h1
          class="text-slate-900 font-extrabold text-4xl sm:text-5xl lg:text-6xl tracking-tight text-center dark:text-white"
        >
          APQ Apple Counter
        </h1>
      </div>
      <div>
        <div class="flex flex-col mt-40 lg:flex-row">
          <div class="basis-full lg:basis-1/2">
            <Counter :countApples="countApples" :run="this.currentRun" />
            <transition name="flashMessage" v-on:after-enter="flashMessage">
              <message v-show="flashMessage" class="text-white text-md">{{
                flashMessage
              }}</message>
            </transition>
          </div>
          <div class="basis-full lg:basis-1/2">
            <div class="flex flex-col lg:place-items-center">
              <div>
                <Statistics :statistics="this.runs" />
                <History :runs="this.runs" :delete-run="deleteRun" />
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import Counter from "./components/Counter.vue";
import History from "./components/History.vue";
import Button from "./components/Button.vue";
import Statistics from "./components/Statistics.vue";
export default {
  components: {
    Counter,
    History,
    Button,
    Statistics,
  },
  data() {
    return {
      runs: [],
      currentRun: { index: 0, apples: [0, 0, 0, 0] },
      flashMessage: null,
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
      this.showFlashMessage("Saved!");
      localStorage.setItem("runs", JSON.stringify(runs));
      this.runs = runs;
      this.initiateNewRun();
    },
    showFlashMessage(msg) {
      this.flashMessage = msg;
      setTimeout(() => (this.flashMessage = null), 1500);
    },
    calculateStats: function () {
      var totalApples = this.runs
        .map((x) => x.apples)
        .flat()
        .reduce((total, cur) => total + cur, 0);
      var message = `I collected a total of ${totalApples} apples`;
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
