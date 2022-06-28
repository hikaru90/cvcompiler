<template>
  <div class="flex items-center justify-center">
    <div class="w-7 h-7 rounded-full relative overflow-hidden shadow-lg">
      <div class="absolute top-0 left-0 w-full h-full bg-gray-100"></div>
      <div
        :style="{ backgroundImage: `url(${image})`, backgroundSize: 'cover' }"
        class="opacity-95 absolute top-0 left-0 w-full h-full"
      ></div>
    </div>
  </div>
</template>

<script>
  import { mapGetters } from "vuex";
  export default {
    computed: {
      ...mapGetters(["image"]),
    },
  };
</script>

<style></style>
