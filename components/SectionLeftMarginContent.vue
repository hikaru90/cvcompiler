<template>
  <div :style="{height: section.margin * 16 + 'px'}" class="w-full">
  </div>
</template>

<script>
import { mapMutations } from 'vuex';

  export default {
    props:{
      section:{
        type: Object,
        required: true,
      },
    },

    methods:{
      ...mapMutations(["updateMargin"]),
      handleInput(field, payload) {
        console.log("handle input");
        this.updateMargin({
          sectionIndex: this.index,
          field: field,
          content: payload,
        });
      },
    },

    mounted(){

    }
  };
</script>

<style></style>
