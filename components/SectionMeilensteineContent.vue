<template>
  <div>
    <div v-for="(element, index) in section.content" :key="'content' + index" class="flex">
      <div class="w-1_5 flex-shrink-0 flex-grow-0 flex items-start justify-center">
        <div :style="{backgroundColor: color}" class="w-1 h-1 text-base mt-02 rounded-xs">
        </div>
      </div>
      <div class="flex-grow">
        <div :style="{color: color}" class="text-base font-bold">
          {{element.heading}}
        </div>
        <div class="text-sm">
          {{element.subheading}}
        </div>
      </div>

      <div v-for="(milestone, idx) in section.content.milestones" :key="index+'milestone'+idx">
        {{milestone}}
      </div>
    </div>
  </div>
</template>

<script>
import { mapGetters } from 'vuex'
  export default {
    props:{
      section: {
        type: Object,
        required: true,
      }
    },

    computed:{
      ...mapGetters(["color"])
    },
  };
</script>

<style></style>
