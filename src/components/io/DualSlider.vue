<template>
  <div class="dual-slider" v-on:mouseup="onmouseupSlider">
    <div class="dual-slider__knob dual-slider__knob--low"
      v-on:mousedown="onmousedownLower"
      v-bind:style="{ left: getLowerPosition }"></div>
    <div class="dual-slider__knob dual-slider__knob--high"
      v-on:mousedown="onmousedownUpper"
      v-bind:style="{ left: getUpperPosition }"></div>
  </div>
</template>

<script>
  export default {
    data: () => ({
      knobLower: { drag: false, value: 0, position: 0, el: undefined },
      knobUpper: { drag: false, value: 500, position: 100, el: undefined },
      min: 0,
      max: 1000
    }),
    computed: {
      getLowerPosition() {
        // let percentage = this.knobLower.value * 100 / this.max - this.min;
        return `${this.knobLower.position}px`;
      },
      getUpperPosition() {
        // let percentage = this.knobUpper.value * 100 / this.max - this.min;
        return `${this.knobUpper.position}px`;
      }
    },
    methods: {
      onmouseup(event) {
        this.knobLower.drag = false;
        this.knobUpper.drag = false;
        document.removeEventListener('mouseup', this.mouseup);
        document.removeEventListener('mousemove', this.onmousemove);
      },
      onmousemove(event) {
        if (!this.knobLower.drag && !this.knobUpper.drag) {
          return;
        }
        event.preventDefault();
        let isSliderTarget = event.target.className === 'dual-slider';

        if (this.knobLower.drag) {
          let sliderTarget = this.knobLower.el.parentNode;
          let sliderOffsetLeft = sliderTarget.offsetLeft;
          let x = event.clientX - sliderOffsetLeft;
          let min = 0;
          let max = this.knobUpper.position;

          if (x >= min && x <= max) {
            this.knobLower.position = x;
          }
        } else if (this.knobUpper.drag) {
          let sliderTarget = this.knobUpper.el.parentNode;
          let sliderOffsetLeft = sliderTarget.offsetLeft;
          let x = event.clientX - sliderOffsetLeft;
          let min = this.knobLower.position;
          let max = sliderTarget.clientWidth;

          if (x >= min && x <= max) {
            this.knobUpper.position = x;
          }
        }
      },
      onmousedownLower(event) {
        this.knobLower.drag = true;
        this.knobLower.el = event.target;
        document.addEventListener('mousemove', this.onmousemove);
        document.addEventListener('mouseup', this.onmouseup);
      },
      onmousedownUpper(event) {
        this.knobUpper.drag = true;
        this.knobUpper.el = event.target;
        document.addEventListener('mousemove', this.onmousemove);
        document.addEventListener('mouseup', this.onmouseup);
      }
    }
  }
</script>

<style scoped>
  .dual-slider {
    border: 1px solid black;
    border-radius: 5px;
    height: 5px;
    margin: 10px 0;
    position: relative;
    width: 100%;
  }

  .dual-slider__knob {
    background: white;
    border: 1px solid black;
    border-radius: 100%;
    height: 15px;
    position: absolute;
    top: 50%;
    transform: translate(-50%, -50%);
    width: 15px;
  }

  .dual-slider__knob:hover {
    cursor: grab;
  }

  .dual-slider__knob--low {
    left: 0%;
    z-index: 0;
  }

  .dual-slider__knob--high {
    left: 100%;
    z-index: 1;
  }
</style>
