<template>
  <div id="a4-container" class="pt-2 w-1/2 fixed ml-1/2 flex items-center justify-center mt-3">
    <div id="a4-canvas" class="bg-white shadow w-42 h-60 rounded-xs text-black px-3 py-6">
      <div>
        <A4Header />
        <A4Content />
      </div>
    </div>
  </div>
</template>

<script>
  import { mapGetters } from "vuex";
  export default {
    computed: {
      ...mapGetters(["fileContent"]),
    },
  };
</script>

<style scoped lang="scss">
  $scale: 16px;
  #a4-canvas {
    font-size: $scale;
  }
  @media print {
    #a4-canvas {
      font-size: $scale*1.2;
    }
  }
</style>
