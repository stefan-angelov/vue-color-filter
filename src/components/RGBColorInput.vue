<template>
  <div class="rgb-selector">
    <label>R:</label>
    <input type="text" 
      maxlength="3" 
      class="rgb-input"
      v-model="red"
      @blur="redTouched = true">
    <label>G:</label>
    <input type="text" 
      maxlength="3" 
      class="rgb-input"
      v-model="green"
      @blur="greenTouched = true">
    <label>B:</label>
    <input type="text" 
      maxlength="3" 
      class="rgb-input"
      v-model="blue"
      @blur="blueTouched = true">
    <button :disabled="!isRgbValid" @click="onSetColor">SET COLOR</button>
    <div v-if="!isRedValid && redTouched">Entered Red Value is not valid!</div>
    <div v-if="!isGreenValid && greenTouched">Entered Green Value is not valid!</div>
    <div v-if="!isBlueValid && blueTouched">Entered Blue Value is not valid!</div>
  </div>
</template>

<script>
import { isValidRgbValue } from '../utils/colorUtils.js';

export default {
  data: function() {
    return {
      red: '',
      green: '',
      blue: '',
      redTouched: false,
      greenTouched: false,
      blueTouched: false
    }
  },
  methods: {
    onSetColor() {
      if(this.isRgbValid) {
        this.$emit('rgbInput', {
          r: +this.red,
          g: +this.green,
          b: +this.blue
        })
      }
    }
  },
  computed: {
    isRedValid: function() {
      return this.red !== '' && isValidRgbValue(this.red);
    },
    isGreenValid: function() {
      return this.green !== '' && isValidRgbValue(this.green);
    },
    isBlueValid: function() {
      return this.blue !== '' && isValidRgbValue(this.blue);
    },
    isRgbValid: function() {
      return this.isRedValid && this.isGreenValid && this.isBlueValid;
    }
  }
}
</script>

<style>
  .rgb-input {
    max-width: 30px;
  }
</style>
