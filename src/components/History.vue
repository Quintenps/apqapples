<template>
  <div class="flex flex-row gap-x-3">
    <div class="flex flex-row gap-x-3">
      <span class="content-center">Run #2</span>

      <CountCell :amount="4" />
      <CountCell :amount="1" />
      <CountCell :amount="3" />
      <CountCell :amount="0" />
    </div>
  </div>
</template>
<script>
import CountCell from "./CountCell.vue";
export default {
  components: { CountCell },
};
</script>
