<template>
  <table class="w-full border-collapse border border-slate-500">
    <thead
      class="text-xs text-gray-700 uppercase bg-gray-50 dark:bg-gray-700 dark:text-gray-400"
    >
      <tr>
        <th scope="col" class="border p-4 border-slate-600">Run</th>
        <th scope="col" class="border p-4 border-slate-600">Round 1</th>
        <th scope="col" class="border p-4 border-slate-600">Round 2</th>
        <th scope="col" class="border p-4 border-slate-600">Round 3</th>
        <th scope="col" class="border p-4 border-slate-600">Round 4</th>
        <th scope="col" class="border p-4 border-slate-600">
          <span class="sr-only">Edit</span>
        </th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="(item, index) in runs" :key="index">
        <td class="border p-4 border-slate-700">
          <span class="content-center">#{{ item.index }}</span>
        </td>
        <td class="border p-4 border-slate-700 text-center">
          {{ item.apples[0] }}
        </td>
        <td class="border p-4 border-slate-700 text-center">
          {{ item.apples[1] }}
        </td>
        <td class="border p-4 border-slate-700 text-center">
          {{ item.apples[2] }}
        </td>
        <td class="border p-4 border-slate-700 text-center">
          {{ item.apples[3] }}
        </td>
        <td
          class="border p-4 border-slate-700 text-center"
          v-on:click="deleteRun(item.index)"
        >
          Delete
        </td>
      </tr>
    </tbody>
  </table>
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
};
</script>
