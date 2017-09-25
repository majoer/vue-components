<template>
  <input class="number-input" type="number" v-bind:value="current"></input>
</template>

<script>
  export default {
    data: () => ({
      min: this.min || 0,
      current: this.current || 0,
      max: this.max || 1
    }),
    props: [ 'min', 'current', 'max' ]
  }
</script>

<style scoped>
  .number-input {
    width: 100%;
  }
</style>
