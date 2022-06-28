<template>
  <div class="mb-1">
    <Card>Content</Card>
    <div class="border border-gray-300 rounded-md p-1 pt-06">
      <div v-for="(section, index) in sections" :key="'section' + index">
        <Section
          :section="section"
          :index="index"
          class="mb-1"
        />
      </div>
      <div
        style="padding: 0.4em 0.75em"
        class="border border-dashed rounded-sm border-gray-400 mt-1 flex items-center justify-center hover:border-green hover:text-green cursor-pointer"
        @click="addSection"
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
      ...mapGetters(["sections"]),
    },
    methods: {
      ...mapMutations(["moveSection", "addSection"]),
      // moveSectionUp(index) {
      //   if (index > 0) {
      //     this.moveSection({ from: index, to: index - 1 });
      //   }
      // },
      // moveSectionDown(index) {
      //   if (index < this.sectionCollection.length) {
      //     this.moveSection({ from: index, to: index + 1 });
      //   }
      // },
    },
    mounted() {
    },
  };
</script>

<style></style>
