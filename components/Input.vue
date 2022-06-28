<template>
  <div>
    <label
      style="line-height: 1.5; font-size: 0.9em; font-weight: 600; margin-bottom: 0.1em"
      class="font-bold block"
    >
      <slot></slot>
    </label>
    <input type="text" :value="value" @input="handleInput($event)" />
  </div>
</template>

<script>
  export default {
    props: {
      value: {
        type: String,
        required: true,
      },
    },
    methods: {
      handleInput(event) {
        this.$emit('handle', event.target.value)
      },
    },
  };
</script>

<style scoped lang="scss">
  input {
    appearance: none;
    border-radius: 0.3em;
    border: 1px solid #cecece;
    box-sizing: border-box;
    background-color: transparent;
    font-size: 0.9em;
    padding: 0.75em;
    display: block;
    width: 100%;
    line-height: 1.2em;
    color: inherit;
    margin: 0;

    &:focus {
      outline: 0;
      border: 1px solid #41b883;
    }
  }
</style>
