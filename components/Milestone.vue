<template>
  <div class="border border-gray-300 rounded-sm mb-05">
    <div class="border-b border-gray-300">
      <div class="flex flex-grow justify-between p-05">
        <div class="flex flex-grow -m-05">
          <Input
            :value="content.heading"
            @handle="handleInput('heading', ...arguments)"
            class="p-05 w-1/5"
            >Titel</Input
          >
          <Input
            :value="content.subheading"
            @handle="handleInput('subheading', ...arguments)"
            class="p-05 w-1/5"
            >Untertitel</Input
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
    <div class="p-05">
      <div v-for="(step, i) in content.milestones" :key="'milestone' + i">
        <Step
          :content="step"
          :sectionIndex="sectionIndex"
          :milestoneIndex="index"
          :stepIndex="i"
        />
      </div>
    </div>
    <div class="p-05">
      <div
        style="padding: 0.4em 0.75em"
        class="border border-dashed rounded-sm border-gray-400 -mt-05 flex items-center justify-center hover:border-green hover:text-green cursor-pointer"
        @click="add"
      >
        + Meilenstein
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
      index: {
        type: Number,
        required: true,
      },
    },
    computed: {
      ...mapGetters(["sections"]),
    },
    methods: {
      ...mapMutations(["updateMilestone", "moveMilestone", "addStep", "deleteMilestone"]),
      add() {
        this.addStep({ sectionIndex: this.sectionIndex, index: this.index });
      },
      handleDelete() {
        this.deleteMilestone({ sectionIndex: this.sectionIndex, index: this.index })
      },
      handleInput(field, payload) {
        console.log("handle input");
        this.updateMilestone({
          sectionIndex: this.sectionIndex,
          index: this.index,
          field: field,
          content: payload,
        });
      },
      shiftUp() {
        if (this.index > 0) {
          this.moveMilestone({
            sectionIndex: this.sectionIndex,
            from: this.index,
            to: this.index - 1,
          });
        }
      },
      shiftDown() {
        if (this.index < this.sections[this.sectionIndex].content.length) {
          this.moveMilestone({
            sectionIndex: this.sectionIndex,
            from: this.index,
            to: this.index + 1,
          });
        }
      },
    },
  };
</script>

<style></style>
