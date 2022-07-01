<template>
  <div class="border border-gray-300 mb-05 rounded-sm m-05">
    <div class="flex flex-grow justify-between mb-05 p-05">
      <div class="flex flex-grow -m-05">
        <Input :value="content.heading" @handle="handleInput('heading', ...arguments)" class="p-05 w-1/5 flex-shrink-0"
          >Titel</Input
        >
        <Textarea
          :value="content.text"
          @handle="handleInput('text', ...arguments)"
          class="p-05 w-full mr-2"
          >Text</Textarea
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
  </div>
</template>

<script>
  import { mapGetters, mapMutations } from "vuex";
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
      index: {
        type: Number,
        required: true,
      },
    },

    computed: {
      ...mapGetters(["sections"]),
    },

    methods: {
      ...mapMutations(["deleteProject", "updateProject", "moveProject"]),
      handleDelete() {
        this.deleteProject({
          sectionIndex: this.sectionIndex,
          milestoneIndex: this.milestoneIndex,
          stepIndex: this.stepIndex,
          index: this.index,
        });
      },
      handleInput(field, payload) {
        console.log("handle input");
        this.updateProject({
          sectionIndex: this.sectionIndex,
          milestoneIndex: this.milestoneIndex,
          stepIndex: this.stepIndex,
          index: this.index,
          field: field,
          content: payload,
        });
      },
      shiftUp() {
        if (this.index > 0) {
          this.moveProject({
            sectionIndex: this.sectionIndex,
            milestoneIndex: this.milestoneIndex,
            stepIndex: this.stepIndex,
            from: this.index,
            to: this.index - 1,
          });
        }
      },
      shiftDown() {
        if (
          this.index <
          this.sections[this.sectionIndex].content[this.milestoneIndex].milestones[this.stepIndex]
            .projects.length
        ) {
          this.moveProject({
            sectionIndex: this.sectionIndex,
            milestoneIndex: this.milestoneIndex,
            stepIndex: this.stepIndex,
            from: this.index,
            to: this.index + 1,
          });
        }
      },
    },
  };
</script>

<style></style>
