<template>
  <div :class="itemAlignment" class="flex">
    <div class="w-1/3 flex-shrink-0 pr-2">
      <slot name="left"></slot>
    </div>
    <div class="w-2/3 flex-shrink-0">
      <slot name="right"></slot>
    </div>
  </div>
</template>

<script>
export default {

  props:{
    itemAlignment: {
      type: String,
      required: false,
      default: 'items-start',
    }
  }

}
</script>

<style>

</style>