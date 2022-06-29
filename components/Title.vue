<template>
  <div class="uppercase font-bold pb-01 mb-05">
    <span class="text-base">
      <slot></slot>
    </span>
    <div :style="{backgroundImage: `url(${require('~/static/line.png')})`, backgroundRepeat: 'no-repeat', backgroundSize: '100% 100%'}" class="w-full h-1px">
    </div>
  </div>
</template>

<script>
export default {

}
</script>

<style>

</style>