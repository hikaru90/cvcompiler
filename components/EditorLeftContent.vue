<template>
  <div class="mb-1">
    <Card>Linker Content</Card>
    <div class="border border-gray-300 rounded-md p-1 pt-06">
      <div v-for="(section, index) in leftSections" :key="section.type+'section' + index">
        <LeftSection
          :section="section"
          :index="index"
          class="mb-1"
        />
      </div>
      <div
        style="padding: 0.4em 0.75em"
        class="border border-dashed rounded-sm border-gray-400 mt-1 flex items-center justify-center hover:border-green hover:text-green cursor-pointer"
        @click="addLeftSection"
      >
        + Section
      </div>
    </div>
  </div>
</template>

<script>
  import { mapGetters, mapMutations } from "vuex";
  export default {
    data() {
      return {
      };
    },
    computed: {
      ...mapGetters(["leftSections"]),
    },
    methods: {
      ...mapMutations(["moveLeftSection", "addLeftSection"]),
    },
    mounted() {
    },
  };
</script>

<style></style>
