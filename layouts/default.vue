<template>
  <div class="h-full w-full">
    <Nuxt />
  </div>
</template>

<script>
export default{

}
</script>

<style lang="scss">
body,
html,
#__nuxt,
#__layout {
  // @apply font-body;
  color: theme("colors.black");
  box-sizing: border-box;
  @apply h-full w-full bg-gray-100;
}
</style>