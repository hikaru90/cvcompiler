<template>
  <div>
    <Title>{{section.title}}</Title>
    <div v-html="section.text" class="text-base mb-1">

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
    },

    computed: {
      // ...mapGetters(["sections"]),
    },

    methods: {

    },
  };
</script>

<style></style>
