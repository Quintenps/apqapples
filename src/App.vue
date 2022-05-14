<template>
  <div id="main" class="container mx-auto px-4">
    <div class="flex flex-col">
      <div class="flex flex-row items-baseline">
        <img src="@/assets/apple.png" class="w-8 h-8" />
        <h1
          class="text-white font-bold text-4xl lg:mt-12 sm:text-5xl lg:text-6xl px-4"
        >
          APQ Apple Counter
        </h1>
      </div>
      <div>
        <div class="flex flex-col lg:mt-16 lg:flex-row">
          <div class="basis-full px-4 lg:basis-1/2">
            <Counter :countApples="countApples" :run="this.currentRun" />
            <transition name="counterMessage">
              <span
                v-show="counterMessage"
                class="text-white italic font-bold text-md"
                >{{ counterMessage }}</span
              >
            </transition>
          </div>
          <div class="basis-full px-4 lg:basis-1/2">
            <div class="flex flex-col lg:place-items-center">
              <div>
                <Actions
                  :runs="this.runs"
                  :currentRun="this.currentRun"
                  :resetStats="resetStats"
                />
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
import History from "./components/Stats/History.vue";
import Button from "./components/Generic/Button.vue";
import Statistics from "./components/Stats/Badges.vue";
import Actions from "./components/Stats/Actions.vue";
export default {
  components: {
    Counter,
    History,
    Button,
    Statistics,
    Actions,
  },
  data() {
    return {
      runs: [],
      currentRun: { index: 0, apples: [0, 0, 0, 0] },
      counterMessage: null,
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
      this.counterMessage = msg;
      setTimeout(() => (this.counterMessage = null), 1500);
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
    resetStats: function () {
      this.runs = [];
      localStorage.setItem("runs", "[]");
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
