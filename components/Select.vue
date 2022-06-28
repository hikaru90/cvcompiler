<template>
  <div>
    <label
      style="line-height: 1.5; font-size: 0.9em; font-weight: 600; margin-bottom: 0.1em"
      class="font-bold block"
    >
      <slot></slot>
    </label>
    <select :name="value" @change="handleInput($event)">
      <template v-for="(option, index) in options">
        <option :value="option.value" :key="'option'+index">{{option.text}}</option>
      </template>
    </select>
  </div>
</template>

<script>
  export default {
    props:{
      options:{
        type: Array,
        required: true,
      },
      value:{
        type: String,
        required: true,
      }
    },
    methods: {
      handleInput(event) {
        this.$emit('handle', event.target.value)
      },
    },
  };
</script>

<style scoped lang="scss">
select {
    appearance: none;
    border-radius: 0.3em;
    border: 1px solid #cecece;
    box-sizing: border-box;
    background-color: transparent;
    font-size: 0.9em;
    padding: 0.75em;
    display: block;
    width: 100%;
    font-weight: 400;
    line-height: 1.2em;
    margin: 0;
    padding-right: 2em;

    &:focus {
      outline: 0;
      border: 1px solid #41b883;
    }
  }
</style>
