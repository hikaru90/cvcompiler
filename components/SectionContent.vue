<template>
  <div class="border border-gray-300 mb-05 rounded-sm m-05 w-full">
    <div class="flex flex-grow justify-between mb-05 p-05">
      <div class="flex flex-grow -m-05">
        <Textarea
          :value="section.text"
          @handle="handleInput('text', ...arguments)"
          class="p-05 w-full"
          >Text</Textarea
        >
      </div>
    </div>
  </div>
</template>

<script>
  import { mapGetters, mapMutations } from "vuex";
  export default {
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
      ...mapMutations(["deleteLeftSection", "updateLeftSection", "moveLeftSection"]),
      handleDelete() {
        this.deleteLeftSection({
          index: this.index,
        });
      },
      handleInput(field, payload) {
        console.log("handle input");
        this.updateLeftSection({
          index: this.index,
          field: field,
          content: payload,
        });
      },
    },
  };
</script>

<style></style>
