<template>
  <div id="a4-container" class="pt-2 w-1/2 flex items-center justify-center mt-3">
    <div
      id="a4-canvas"
      class="bg-white shadow w-42 min-h-60 rounded-xs text-black px-3 py-6 relative"
    >
      <div>
        <A4Header />
        <A4Content />
      </div>
      <div
        v-for="(number, index) in pageCount"
        :key="'page' + number"
        class="absolute text-base right-0"
        :style="{ top: pageHeight  * (index + 1) - 40 + 'px' }"
      >
        {{ index + 1 }} / {{ pageCount }}
      </div>
    </div>
  </div>
</template>

<script>
  import { mapGetters } from "vuex";
  export default {
    data(){
      return{
        pageHeight: 930,
        pageCount: 0,
      }
    },

    computed: {
      ...mapGetters(["fileContent"]),
    },

    methods: {
      count() {
        console.log('count');
        try {
          if (document) {
            const res = document.getElementById("a4-canvas").scrollHeight / this.pageHeight;
            console.log("pageCount", res);
            this.pageCount = Math.ceil(res);
          }
        } catch {}
      },
      // handleResize(){

      // }
    },

    mounted() {
      this.count();
    },
    beforeMount() {
      var ro = new ResizeObserver((entries) => {
        for (let entry of entries) {
          const cr = entry.contentRect;
          this.count()
        }
      });
      ro.observe(document.querySelector('#a4-canvas'));
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
      font-size: $scale * 1.2;
    }
  }
</style>
