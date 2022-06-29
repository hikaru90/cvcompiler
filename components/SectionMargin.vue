<template>
  <div class="flex-grow">
    <Input :value="margin" @handle="handleInput('margin', ...arguments)" class="p-05 w-full"
      >Abstand</Input
    >
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
      index:{
        type: Number,
        required: true,
      },
    },

    computed:{
      margin(){
        if(this.section.margin){
          return this.section.margin
        }
        return '0'
      }
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
