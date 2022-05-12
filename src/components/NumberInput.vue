<template>
  <input
    type="number"
    class="form-control block w-full px-3 py-1.5 text-base font-normal text-gray-700 bg-white bg-clip-padding border border-solid border-gray-300 rounded transition ease-in-out m-0 focus:text-gray-700 focus:bg-white focus:border-blue-600 focus:outline-none"
    :name="{ name }"
<<<<<<< HEAD
    :value="{ modelValue }"
=======
    :value="{ amount }"
>>>>>>> 4d346697d70fe83051e00cfcf84569a3f44cce8a
  />
</template>
<script>
export default {
  props: {
    name: String,
<<<<<<< HEAD
    modelValuel: Number,
=======
    amount: {
      type: Number,
      default: 0,
    },
>>>>>>> 4d346697d70fe83051e00cfcf84569a3f44cce8a
  },
};
</script>
