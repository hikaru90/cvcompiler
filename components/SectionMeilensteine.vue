<template>
  <div class="w-full p-05">
    <div v-for="(milestone, idx) in section.content" :key="'milestone'+idx">
      <Milestone :content="milestone" :sectionIndex="index" :index="idx" />
    </div>

    <div
      style="padding: 0.4em 0.75em"
      class="border border-dashed rounded-sm border-gray-400 mt-1 flex items-center justify-center hover:border-green hover:text-green cursor-pointer"
      @click="add"
    >
      + Station
    </div>
  </div>
</template>

<script>
  import { mapGetters, mapMutations } from "vuex";
  export default {
    props:{
      index:{
        type: Number,
        required: true,
      },
      section:{
        type: Object,
        required: true,
      }
    },
    methods: {
      ...mapMutations(["addMilestone"]),
      add() {
        this.addMilestone({index: this.index})
      },
    },
  };
</script>

<style></style>
