<template>
  <div>
    <h3
      class="text-slate-900 font-bold uppercase tracking-tight dark:text-white"
    >
      Latest Runs
    </h3>
    <TransitionGroup tag="div" class="transition-all" name="history">
      <div
        v-for="run in runs"
        class="flex flex-row gap-4 my-2"
        :key="run.index"
      >
        <div class="w-24">Run #{{ run.index }}</div>
        <div class="py-0 px-2 rounded-md" :class="colorcell(run.apples[0])">
          {{ run.apples[0] }}
        </div>
        <div class="py-0 px-2 rounded-md" :class="colorcell(run.apples[1])">
          {{ run.apples[1] }}
        </div>
        <div class="py-0 px-2 rounded-md" :class="colorcell(run.apples[2])">
          {{ run.apples[2] }}
        </div>
        <div class="py-0 px-2 rounded-md" :class="colorcell(run.apples[3])">
          {{ run.apples[3] }}
        </div>
        <div
          v-on:click="deleteRun(run.index)"
          class="cursor-pointer text-slate-500 hover:text-red-500 flex justify-center items-center"
        >
          <svg
            xmlns="http://www.w3.org/2000/svg"
            class="h-5 w-5"
            viewBox="0 0 20 20"
            fill="currentColor"
          >
            <path
              fill-rule="evenodd"
              d="M9 2a1 1 0 00-.894.553L7.382 4H4a1 1 0 000 2v10a2 2 0 002 2h8a2 2 0 002-2V6a1 1 0 100-2h-3.382l-.724-1.447A1 1 0 0011 2H9zM7 8a1 1 0 012 0v6a1 1 0 11-2 0V8zm5-1a1 1 0 00-1 1v6a1 1 0 102 0V8a1 1 0 00-1-1z"
              clip-rule="evenodd"
            />
          </svg>
        </div>
      </div>
    </TransitionGroup>
  </div>
</template>
<script>
export default {
  props: {
    runs: {
      type: Object,
    },
    deleteRun: {
      type: Function,
    },
  },
  methods: {
    colorcell(value) {
      if (value > 0 && value < 3) {
        return "bg-green-300";
      } else if (value > 2) {
        return "bg-yellow-300";
      }
      return "bg-gray-200";
    },
  },
};
</script>
