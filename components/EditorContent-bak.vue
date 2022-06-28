<template>
  <div class="mb-1">
    <Card>Content</Card>
    <div class="border border-gray-300 rounded-md p-1 pt-06">
      <div v-for="(section, index) in sectionCollection" :key="'section' + index">
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
  import { mapFields } from "vuex-map-fields";
  export default {
    data() {
      return {
        cacheBusting: "",
        sectionCollection: [],
      };
    },
    watch: {
      sectionCollection: {
        handler(newValue, oldValue) {
          this.setSections(JSON.stringify(newValue));
        },
        deep: true,
      },
      // skillset() {
      //   this.initSkills();
      //   console.log("JSON.parse(this.skillset)", JSON.parse(this.skillset));
      // },
    },
    computed: {
      ...mapGetters(["sections"]),
    },
    methods: {
      ...mapMutations(["moveSection", "setSections"]),
      update(index, payload) {
        // console.log("index", index);
        // const value = JSON.parse(JSON.stringify(payload.payload));
        this.sectionCollection[index] = payload
      },
      initSections() {
        this.sectionCollection = JSON.parse(this.sections);
      },
      // deleteSkill(index){
      //   console.log('index', index);
      //   console.log('type', typeof index);
      //   this.skills.splice(index, 1)
      // },
      addSection(payload) {
        this.sectionCollection.push({ type: "section", title: "Work Experience" });
      },
      moveSectionUp(index) {
        if (index > 0) {
          this.moveSection({ from: index, to: index - 1 });
        }
      },
      moveSectionDown(index) {
        if (index < this.sectionCollection.length) {
          this.moveSection({ from: index, to: index + 1 });
        }
      },
    },
    mounted() {
      this.initSections();
    },
  };
</script>

<style></style>
