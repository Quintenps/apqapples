<template>
  <span
    class="w-fit bg-gray-100 text-gray-800 font-medium items-center px-2.5 py-0.5 rounded mr-2 dark:bg-gray-700 dark:text-gray-300"
  >
    <p>
      <span class="font-extrabold">{{ statsValue }}</span>
      {{ statsDescription }}
    </p>
  </span>
</template>
<script>
export default {
  props: {
    statsValue: {
      type: Number,
      default: 0,
    },
    statsDescription: {
      type: String,
    },
  },
};
</script>
