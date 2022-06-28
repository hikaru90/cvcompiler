<template>
  <div class="mb-1">
    <Card>Fertigkeiten</Card>
    <div class="border border-gray-300 rounded-md p-1 pt-06">
      <div v-for="(skill, index) in skills" :key="cacheBusting + 'skill' + index">
        <Skill
          @reskill="reskill(index, ...arguments)"
          @delete="deleteSkill(index)"
          @up="up(index)"
          @down="down(index)"
          :name="skill.name"
          :proficiency="skill.proficiency"
          :duration="skill.duration"
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
        skills: [],
      };
    },
    watch: {
      skills: {
        handler(oldValue, newValue) {
          this.setSkillset(JSON.stringify(this.skills));
        },
        deep: true,
      },
      skillset() {
        this.initSkills();
        console.log("JSON.parse(this.skillset)", JSON.parse(this.skillset));
      },
    },
    computed: {
      ...mapGetters(["skillset"]),
    },
    methods: {
      ...mapMutations(["setSkillset"]),
      reskill(index, payload) {
        console.log("index", index);
        const value = JSON.parse(JSON.stringify(payload.payload));
        this.skills[index][payload.field] = value
      },
      initSkills() {
        this.skills = JSON.parse(this.skillset);
      },
      addSkill(){
        this.skills.push({"name":"Name", "proficiency": "Prozent", "duration": "5+"})
      },
      deleteSkill(index){
        console.log('index', index);
        console.log('type', typeof index);
        this.skills.splice(index, 1)
      },
      move(from,to){
        this.skills.splice(to, 0, this.skills.splice(from, 1)[0]);
      },
      up(index){
        if(index>0){
          this.move(index,index-1)
        }
      },
      down(index){
        if(index<this.skills.length){
          this.move(index,index+1)
        }
      },
    },
    mounted() {
      this.initSkills();
    },
  };
</script>

<style></style>
