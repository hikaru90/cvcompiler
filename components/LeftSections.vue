<template>
  <div class="flex-grow">
    <div v-for="(section, index) in leftSections" :key="section.type+'section' + index" class="">
      
      <component :is="section.type+'Content'" :section="section"></component>
      
    </div>
  </div>
</template>

<script>
  import { mapGetters } from "vuex";
  export default {
    computed: {
      ...mapGetters(["leftSections"]),
    },
  };
</script>

<style></style>
