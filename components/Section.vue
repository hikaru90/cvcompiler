<template>
  <div>
    <div class="w-full bg-gray-600 rounded-t-sm px-05 py-02">
      <span class="text-md text-white font-bold"> Section </span>
    </div>
    <div class="border-2 border-gray-600 mb-05 rounded-b-sm">
      <div class="flex flex-grow justify-between border-b border-gray-300 p-05">
        <div class="flex flex-grow -m-05">
          <Input
            :value="section.title"
            @handle="handleInput('title', ...arguments)"
            class="p-05 w-1/5"
            >Titel</Input
          >
          <Select
            :value="section.type"
            @handle="handleInput('type', ...arguments)"
            :options="[{value: 'SectionMeilensteine', text: 'Meilensteine'},{value: 'SectionMargin', text: 'Margin'}]"
            class="p-05 w-1/5"
            >Typ</Select
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
      <div class="p-05">
        <div class="flex flex-grow -m-05">
          <component :is="section.type" :index="index" :section="section" ></component>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  import { mapGetters, mapMutations } from "vuex";
  export default {
    data() {
      return {};
    },

    props: {
      section: {
        type: Object,
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
      ...mapMutations(["updateSection", "moveSection", "deleteSection"]),
      handleInput(field, payload) {
        this.updateSection({ index: this.index, field: field, content: payload });
      },
      handleDelete() {
        this.deleteSection({index: this.index})
      },
      shiftUp() {
        if (this.index > 0) {
          this.moveSection({ from: this.index, to: this.index - 1 });
        }
      },
      shiftDown() {
        if (this.index < this.sections.length) {
          this.moveSection({ from: this.index, to: this.index + 1 });
        }
      },
    },

    mounted() {
      // this.sectionContent.title = "Work Experience";
    },
  };
</script>

<style></style>
