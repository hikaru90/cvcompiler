<template>
  <div class="border border-gray-300 mb-05 rounded-sm">
    <div class="flex flex-grow justify-between mb-05 p-05">
      <div class="flex flex-grow -m-05">
        <Input
          :value="content.date"
          @handle="handleInput('date', ...arguments)"
          class="p-05 w-1/5"
          >Datum</Input
        >
        <Input
          :value="content.title"
          @handle="handleInput('title', ...arguments)"
          class="p-05 w-1/5"
          >Jobtitel</Input
        >
      </div>
      <div class="flex">
        <div
          @click="shiftUp"
          class="mt-1_7 border border-gray-300 rounded-sm flex items-center justify-center w-2 h-2 cursor-pointer mr-05"
        >
          <span class="text-md mb-01"> ▲ </span>
        </div>
        <div
          @click="shiftDown"
          class="mt-1_7 border border-gray-300 rounded-sm flex items-center justify-center w-2 h-2 cursor-pointer mr-05"
        >
          <span class="text-md mt-01"> ▼ </span>
        </div>
        <div
          @click="handleDelete"
          class="mt-1_7 bg-red rounded-sm flex items-center justify-center w-2 h-2 cursor-pointer text-white"
        >
          <span class="text-md"> ╳ </span>
        </div>
      </div>
    </div>
    <div>
      <div v-for="(project, j) in content.projects" :key="'project'+j">
        <Project :content="project" :sectionIndex="sectionIndex" :milestoneIndex="milestoneIndex" :stepIndex="stepIndex" :index="j" />
      </div>
    </div>
    <div class="p-05">
      <div
        style="padding: 0.4em 0.75em"
        class="border border-dashed rounded-sm border-gray-400 -mt-05 flex items-center justify-center hover:border-green hover:text-green cursor-pointer"
        @click="add"
      >
        + Projekt
      </div>
    </div>
  </div>
</template>

<script>
import { mapGetters, mapMutations } from 'vuex';

  export default {
    props: {
      content: {
        type: Object,
        required: true,
      },
      sectionIndex: {
        type: Number,
        required: true,
      },
      milestoneIndex: {
        type: Number,
        required: true,
      },
      stepIndex: {
        type: Number,
        required: true,
      },
    },

    computed:{
      ...mapGetters(["sections"]),
    },

    methods:{
      ...mapMutations(["deleteStep", "updateStep", "moveStep", "addProject"]),
      add() {
        this.addProject({ sectionIndex: this.sectionIndex, milestoneIndex: this.milestoneIndex, stepIndex: this.stepIndex });
      },
      handleDelete() {
        this.deleteStep({ sectionIndex: this.sectionIndex, milestoneIndex: this.milestoneIndex, stepIndex: this.stepIndex })
      },
      handleInput(field, payload) {
        console.log("handle input");
        this.updateStep({
          sectionIndex: this.sectionIndex,
          milestoneIndex: this.milestoneIndex,
          stepIndex: this.stepIndex,
          field: field,
          content: payload,
        });
      },
      shiftUp() {
        if (this.stepIndex > 0) {
          this.moveStep({
            sectionIndex: this.sectionIndex,
            milestoneIndex: this.milestoneIndex,
            from: this.stepIndex,
            to: this.stepIndex - 1,
          });
        }
      },
      shiftDown() {
        if (this.stepIndex < this.sections[this.sectionIndex].content[this.milestoneIndex].milestones.length) {
          this.moveStep({
            sectionIndex: this.sectionIndex,
            milestoneIndex: this.milestoneIndex,
            from: this.stepIndex,
            to: this.stepIndex + 1,
          });
        }
      },
    },
  };
</script>

<style></style>
