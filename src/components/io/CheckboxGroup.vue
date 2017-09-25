<template>
  <div class="checkbox-group">
    <div class="checkbox-group__checkbox" v-for="(entry, index) in entries">
      <label class="checkbox-group__checkbox__label" v-bind:for="createCheckboxId(entry, index)">{{ entry.name }}</label>
      <input class="checkbox-group__checkbox__input" v-bind:id="createCheckboxId(entry, index)"  v-bind:value="entry.value" type="checkbox"></input>
    </div>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        entries: [
          { name: 'volte', value: true },
          { name: '4g', value: false },
          { name: '5g', value: true },
          { name: '5g', value: true },
          { name: '5g', value: true },
          { name: '5g', value: true },
          { name: '5g', value: true },
          { name: '5g', value: true },
          { name: '5g', value: true },
          { name: '5g', value: true },
        ]
      }
    },
    methods: {
      createCheckboxId: (entry, index) => {
        return `${index}_${entry.name}`;
      }
    }
  }
</script>

<style scoped>
  .checkbox-group {
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
    width: 100%;
  }

  .checkbox-group__checkbox {
    display: flex;
    flex-basis: 20%;
  }

  .checkbox-group__checkbox__label {
    flex-grow: 1;
    text-align: right;
  }

  .checkbox-group__checkbox__input {

  }
</style>
