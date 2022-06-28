<template>
  <div class="flex-grow">
    <div v-for="(section, index) in sections" :key="'section' + index" class="">
      <Title>{{section.title}}</Title>

      <component :is="section.type+'Content'" :section="section" ></component>
      
    </div>
  </div>
</template>

<script>
  import { mapGetters } from "vuex";
  export default {
    computed: {
      ...mapGetters(["sections"]),
    },
  };
</script>

<style></style>
