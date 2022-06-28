<template>
<div>
  <div class="font-bold text-lg uppercase -ml-02 pl-1px">
    {{name}}
  </div>
  <div :style="{color: color}" class="text-md">
    {{education}}
  </div>
</div>
</template>

<script>
import { mapGetters } from 'vuex'
export default {
  computed:{
    ...mapGetters(["name", "education", "color"])
  }

}
</script>

<style>

</style>