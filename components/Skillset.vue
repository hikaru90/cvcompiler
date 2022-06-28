<template>
  <div>
    <div v-for="(skill, index) in JSON.parse(skillset)" :key="'skill'+index">
    <div class="mb-05">

      <div class="flex justify-between text-base mb-03">
        <div>
          {{skill.name}}
        </div>
        <div>
          {{skill.duration}}
        </div>
      </div>
      <div class="h-03 w-full relative">
        <div class="h-full w-full bg-gray-200 absolute top-0 left-0 rounded-xs"></div>
        <div :style="{backgroundColor: color, width: skill.proficiency + '%'}" class="h-03 absolute top-0 left-0 rounded-xs"></div>
      </div>
    </div>
        </div>

  </div>
</template>

<script>
import {mapGetters} from 'vuex'
export default {
  computed:{
    ...mapGetters(["skillset", "color"]),
  },
  methods:{
  }
}
</script>

<style>

</style>