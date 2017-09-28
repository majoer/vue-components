<template>
  <div>
    <div class="price"><InputSlider></InputSlider></div>
    <div class="feature"><CheckboxGroup></CheckboxGroup></div>
    <div class="feature"><Select></Select></div>
    <div class="feature"><Toggle></Toggle></div>
  </div>
</template>

<script>
  import InputSlider from '../io/InputSlider';
  import CheckboxGroup from '../io/CheckboxGroup';
  import Select from '../io/Select';
  import Toggle from '../io/Toggle';

  export default {
    components: {
      Toggle,
      Select,
      CheckboxGroup,
      InputSlider
    }
  }
</script>

<style scoped>
</style>
