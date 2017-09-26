<template>
  <input class="number-input" type="number"
    v-on:blur="onBlur"
    v-on:input="onInput"
    v-bind:value="value"
    v-bind:min="min"
    v-bind:max="max"></input>
</template>

<script>
  export default {
    props: [ 'min', 'value', 'max' ],
    methods: {
      onBlur(event) {
        let newValue = event.target.closest('input').value;
        this.updateValue(newValue);
      },
      onInput(event) {
        let newValue = event.target.closest('input').value;
        let difference = Math.abs(newValue - this.value);

        if (difference === 1) {
          this.updateValue(newValue);
        }
      },
      updateValue(newValue) {
        if (newValue < this.min) {
          this.value = this.min + 1;
          this.value = this.min;
        } else if (newValue > this.max) {
          this.value = this.max - 1;
          this.value = this.max;
        } else {
          this.value = newValue;
        }

        this.$emit('input', Number(this.value));
      }
    }
  }
</script>

<style scoped>
  .number-input {
    width: 100%;
  }
</style>
