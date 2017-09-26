<template>
  <div class="input-slider">
    <div class="input-slider__slider">
      <DualSlider v-bind:min="min"
        v-bind:valueLower="value.lower"
        v-bind:valueUpper="value.upper"
        v-bind:max="max"
        v-on:inputLower="valueLower => value.lower = valueLower"
        v-on:inputUpper="valueUpper => value.upper = valueUpper"></DualSlider>
    </div>
    <div class="input-slider__input__low">
      <NumberInput v-bind:min="min" v-model="value.lower" v-bind:max="value.upper"></NumberInput>
    </div>
    <div class="input-slider__input__high">
      <NumberInput v-bind:min="value.lower" v-model="value.upper" v-bind:max="max"></NumberInput>
    </div>
  </div>
</template>

<script>
  import Slider from '../io/Slider';
  import NumberInput from '../io/NumberInput';
  import DualSlider from '../io/DualSlider';

  export default {
    components: {
      DualSlider,
      Slider,
      NumberInput
    },
    data: () => ({
      min: 0,
      value: {
        lower: 0,
        upper: 500
      },
      max: 1000
    })
  }
</script>

<style scoped>
  .input-slider {
    cursor: pointer;
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
    justify-content: space-around;
  }

  .input-slider__slider {
    display: flex;
    flex-grow: 1;
    flex-basis: 100%;
  }

  .input-slider__slider__low,
  .input-slider__slider__high {
    flex-grow: 0.5;
  }

  .input-slider__input__high,
  .input-slider__input__low {
    flex-basis: 40%;
    flex-grow: 0;
  }
</style>
