<template>
  <div class="input-slider">
    <div class="input-slider__slider">
      <DualSlider></DualSlider>
    </div>
    <div class="input-slider__input__low">
      <NumberInput v-bind:min="min" v-bind:current="currentLower" v-bind:max="currentHigher"></NumberInput>
    </div>
    <div class="input-slider__input__high">
      <NumberInput v-bind:min="currentLower" v-bind:current="currentHigher" v-bind:max="max"></NumberInput>
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
      currentLower: 0,
      currentHigher: 500,
      max: 1000
    })
  }
</script>

<style scoped>
  .input-slider {
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
