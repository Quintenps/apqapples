<template>
  <div id="main" class="container mx-auto px-4">
    <div class="flex flex-col">
      <div>
        <h1 class="text-2xl font-bold underline">APQ Apple Counter</h1>
      </div>
      <div>
        <div class="flex flex-col lg:flex-row">
          <div class="basis-full lg:basis-2/5">
            <Counter />
          </div>
          <div class="basis-full lg:basis-3/5">
            <History class="place-content-center" />
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import Counter from "./components/Counter.vue";
import History from "./components/History.vue";
export default {
  components: {
    Counter,
    History,
  },
};
</script>
