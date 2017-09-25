<template>
  <input class="slider" type="range" v-bind:min="min" v-bind:value="current" v-on:input="updateValue" v-bind:max="max"></input>
</template>

<script>
  export default {
    data: () => ({
      min: this.min || 0,
      current: this.current || 0,
      max: this.max || 1
    }),
    methods: {
      updateValue(event) {
        this.$emit('input', Number(event.target.value));
      }
    },
    props: [ 'min', 'current', 'max' ],
  }
</script>

<style scoped>
  .slider {
    width: 100%;
  }
</style>
