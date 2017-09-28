<template>
  <div class="dual-slider" v-on:mouseup="onmouseupSlider" v-on:click.self="onclickSlider">
    <div class="dual-slider__knob dual-slider__knob--lower"
      v-on:mousedown="onmousedownLower"
      v-on:change="updateLowerValue"
      v-bind:style="{ left: getLowerPosition }"><span class="dual-slider__knob__text">&lt;</span></div>
    <div class="dual-slider__knob dual-slider__knob--upper"
      v-on:mousedown="onmousedownUpper"
      v-on:change="updateUpperValue"
      v-bind:style="{ left: getUpperPosition }"><span class="dual-slider__knob__text">&gt;</span></div>
  </div>
</template>

<script>
  export default {
    props: [ 'min', 'valueLower', 'valueUpper', 'max' ],
    data: () => ({
      elSlider: undefined,
      knobLowerDrag: false,
      knobUpperDrag: false,
      min: 0,
      max: 1000
    }),
    computed: {
      getLowerPosition() {
        if (!this.elSlider) {
          return '0%';
        }

        let x = 100 / (this.max - this.min) * this.valueLower;

        return `${x}%`;
      },
      getUpperPosition() {
        if (!this.elSlider) {
          return '100%';
        }

        let x = 100 / (this.max - this.min) * this.valueUpper;

        return `${x}%`;
      }
    },
    methods: {
      onmouseup(event) {
        this.isKnobDragLower = false;
        this.isKnobDragUpper = false;
        document.removeEventListener('mouseup', this.mouseup);
        document.removeEventListener('mousemove', this.onmousemove);
      },
      onmousemove(event) {
        if (!this.isKnobDragLower && !this.isKnobDragUpper) {
          return;
        }
        event.preventDefault();
        let isSliderTarget = event.target.className === 'dual-slider';

        if (this.isKnobDragLower) {
          let newLowerValue = this.calculateValueFromMouseEvent(event);

          if (this.valueLower === newLowerValue) {
            return;
          }

          if (newLowerValue < this.min) {
            newLowerValue = this.min;
          } else if (newLowerValue > this.valueUpper) {
            newLowerValue = this.valueUpper;
          }

          this.valueLower = newLowerValue;
          this.$emit('inputLower', this.valueLower);
        } else if (this.isKnobDragUpper) {
          let newUpperValue = this.calculateValueFromMouseEvent(event);

          if (this.valueUpper === newUpperValue) {
            return;
          }

          if (newUpperValue < this.valueLower) {
            newUpperValue = this.valueLower;
          } else if (newUpperValue > this.max) {
            newUpperValue = this.max;
          }

          this.valueUpper = newUpperValue;
          this.$emit('inputUpper', this.valueUpper);
        }
      },
      calculateValueFromMouseEvent(event) {
        let sliderWidth = this.elSlider.clientWidth;
        let sliderOffsetLeft = this.elSlider.offsetLeft;
        let x = 100 * (event.clientX - sliderOffsetLeft) / sliderWidth;

        return  Math.round(x * (this.max - this.min) / 100);
      },
      onmousedownLower(event) {
        this.isKnobDragLower = true;
        document.addEventListener('mousemove', this.onmousemove);
        document.addEventListener('mouseup', this.onmouseup);
      },
      onmousedownUpper(event) {
        this.isKnobDragUpper = true;
        document.addEventListener('mousemove', this.onmousemove);
        document.addEventListener('mouseup', this.onmouseup);
      },
      onclickSlider(event) {
        let valueAtMouseClick = this.calculateValueFromMouseEvent(event);
        let diffLower = Math.abs(this.valueLower - valueAtMouseClick);
        let diffUpper = Math.abs(this.valueUpper - valueAtMouseClick);

        if (diffLower <= diffUpper) {
          this.valueLower = valueAtMouseClick;
          this.$emit('inputLower', this.valueLower);
        } else if (diffLower > diffUpper) {
          this.valueUpper = valueAtMouseClick;
          this.$emit('inputUpper', this.valueUpper);
        }
      }
    },
    mounted() {
      this.elSlider = document.querySelector('.dual-slider');
      this.elKnobLower = document.querySelector('.dual-slider__knob--lower');
      this.elKnobUpper = document.querySelector('.dual-slider__knob--upper');
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
    user-select: none;
    width: 100%;
  }

  .dual-slider__knob {
    background: white;
    border: 1px solid black;
    border-radius: 100%;
    font-size: 14px;
    height: 15px;
    position: absolute;
    top: 50%;
    transform: translate(-50%, -50%);
    width: 15px;
  }

  .dual-slider__knob__text {
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
  }

  .dual-slider__knob:hover {
    cursor: grab;
  }

  .dual-slider__knob--lower {
    left: 0%;
    z-index: 0;
  }

  .dual-slider__knob--upper {
    left: 100%;
    z-index: 1;
  }
</style>
