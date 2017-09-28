<template>
  <div class="toggle">
    <button class="toggle__on" v-on:click="on" v-bind:class="{ 'toggle__on--active': value }">on</button>
    <div class="toggle__separator"></div>
    <button class="toggle__off" v-on:click="off" v-bind:class="{ 'toggle__off--active': !value }">off</button>
  </div>
</template>

<script>
export default {
  data: () => ({
    value: false
  }),
  methods: {
    on() {
      this.value = true;
    },
    off() {
      this.value = false;
    }
  }
}
</script>

<style scoped>
  .toggle {
    border: 1px solid black;
    border-radius: 3px;
    display: flex;
    height: 1em;
    line-height: 0;
    overflow: hidden;
    white-space: nowrap;
    width: 42px;
  }

  .toggle__separator {
    border-left: 1px solid black;
    width: 0;
  }

  .toggle__on,
  .toggle__off {
    border: none;
    background: none;
    cursor: pointer;
    flex-basis: 50%;
    flex-grow: 0.5;
    height: 100%;
    line-height: 0;
    padding: 0;
    user-select: none;
  }

  .toggle__on--active,
  .toggle__off--active {
    background: #ff6600;
  }
</style>
