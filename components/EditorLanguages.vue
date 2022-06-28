<template>
  <div class="mb-1">
    <Card>Sprachen</Card>
    <div class="border border-gray-300 rounded-md p-1 pt-06">
      <div v-for="(skill, index) in languages" :key="cacheBusting + 'skill' + index">
        <Skill
          @reskill="reskill(index, ...arguments)"
          @delete="deleteSkill(index)"
          @up="up(index)"
          @down="down(index)"
          :name="skill.name"
          :proficiency="skill.proficiency"
          :duration="skill.level"
        />
      </div>
      <div
        style="padding: 0.4em 0.75em"
        class="border border-dashed rounded-sm border-gray-400 mt-1 flex items-center justify-center hover:border-green hover:text-green cursor-pointer"
        @click="addSkill"
      >
        +
      </div>
    </div>
  </div>
</template>

<script>
  import { mapGetters, mapMutations } from "vuex";
  import { mapFields } from "vuex-map-fields";
  export default {
    data() {
      return {
        cacheBusting: "",
        languages: [],
      };
    },
    watch: {
      languages: {
        handler(oldValue, newValue) {
          this.setLanguageset(JSON.stringify(this.languages));
        },
        deep: true,
      },
      languageset() {
        this.initLanguages();
        console.log("JSON.parse(this.languageset)", JSON.parse(this.languageset));
      },
    },
    computed: {
      ...mapGetters(["languageset"]),
    },
    methods: {
      ...mapMutations(["setLanguageset"]),
      reskill(index, payload) {
        console.log("index", index);
        const value = JSON.parse(JSON.stringify(payload.payload));
        this.languages[index][payload.field] = value
      },
      initLanguages() {
        this.languages = JSON.parse(this.languageset);
      },
      addSkill(){
        this.languages.push({"name":"Name", "proficiency": "Prozent", "duration": "5+"})
      },
      deleteSkill(index){
        console.log('index', index);
        console.log('type', typeof index);
        this.languages.splice(index, 1)
      },
      move(from,to){
        this.languages.splice(to, 0, this.languages.splice(from, 1)[0]);
      },
      up(index){
        if(index>0){
          this.move(index,index-1)
        }
      },
      down(index){
        if(index<this.languages.length){
          this.move(index,index+1)
        }
      },
    },
    mounted() {
      this.initLanguages();
    },
  };
</script>

<style></style>
