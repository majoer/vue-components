<template>
  <div>
    <select class="select">
      <option class="select__option" v-for="entry in entries" v-bind:value="entry.value">
        {{ entry.name }}
      </option>
    </select>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        entries: [
          {
            name: 'volte',
            value: true
          },
          {
            name: '4g',
            value: false
          },
          {
            name: '5g',
            value: true
          }
        ]
      }
    }
  }
</script>

<style scoped>
</style>
