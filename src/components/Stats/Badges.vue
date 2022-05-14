<template>
  <div>
    <h3 class="text-white font-bold uppercase tracking-tight mt-6 mb-2">
      Statistics
    </h3>
    <div class="flex flex-col gap-2">
      <Badge :statsValue="statistics.length" statsDescription="runs done" />
      <Badge
        :statsValue="calculateTotalApples()"
        statsDescription="apples gathered"
      />
      <Badge
        :statsValue="calculateMostApplesInARound()"
        statsDescription="most apples gathered in a round"
      />
      <Badge
        :statsValue="calculateMostApplesInARun()"
        statsDescription="most apples gathered in a run"
      />
    </div>
  </div>
</template>
<script>
import Badge from "../Generic/Badge.vue";
export default {
  props: {
    statistics: {
      type: Object,
    },
  },
  components: { Badge },
  methods: {
    calculateTotalApples: function () {
      return this.statistics
        .map((x) => x.apples)
        .flat()
        .reduce((total, cur) => total + cur, 0);
    },
    calculateMostApplesInARound: function () {
      var roundValues = this.statistics.flatMap((x) => x.apples);
      return Math.max(0, ...roundValues);
    },
    calculateMostApplesInARun: function () {
      var roundValues = this.statistics.map((x) => x.apples);
      var maxSum = 0;
      roundValues.reduce((total, cur) => {
        var totalValue = cur.reduce((x, y) => x + y, 0);
        maxSum = totalValue > maxSum ? totalValue : maxSum;
      }, 0);

      return maxSum;
    },
  },
};
</script>
