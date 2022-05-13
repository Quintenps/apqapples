<template>
  <div>
    <h3
      class="text-slate-900 font-bold uppercase tracking-tight dark:text-white"
    >
      Statistics
    </h3>
    <div class="grid grid-cols-4">
      <StatisticsTile
        :statsValue="statistics.length"
        statsDescription="runs done"
      />
      <StatisticsTile
        :statsValue="calculateTotalApples()"
        statsDescription="apples gathered"
      />
      <StatisticsTile
        :statsValue="calculateMostApplesInARun()"
        statsDescription="most apples gathered in a round"
      />
      <StatisticsTile
        :statsValue="calculateTotalApples()"
        statsDescription="most apples gathered in a run"
      />
    </div>
  </div>
</template>
<script>
import StatisticsTile from "./StatisticsTile.vue";
export default {
  props: {
    statistics: {
      type: Object,
    },
  },
  components: { StatisticsTile },
  methods: {
    calculateTotalApples: function () {
      return this.statistics
        .map((x) => x.apples)
        .flat()
        .reduce((total, cur) => total + cur, 0);
    },
    calculateMostApplesInARun: function () {
      var roundValues = this.statistics.flatMap((x) => x.apples);
      return Math.max(...roundValues);
    },
    calculateMostApplesInARound: function () {
      var roundValues = this.statistics.flatMap((x) => x.apples);
      return Math.max(...roundValues);
    },
  },
};
</script>
