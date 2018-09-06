<template>
  <div class="hex-selector">
    <span>#</span>
    <input type="text" maxlength="6" v-model="input">
    <button @click="onSetColor" :disabled="!isColorValid">SET COLOR</button>
    <div v-if="!isColorValid && input">Entered HEX Color is not valid!</div>
  </div>
</template>

<script>
import { isValidHexColor } from '../utils/colorUtils.js';

export default {
  data: function() {
    return {
      input: ''
    }
  },
  methods: {
    onSetColor() {
      if(this.isColorValid) {
        this.$emit('hexInput', '#' + this.input);
      }
    }
  },
  computed: {
    isColorValid: function() {
      return isValidHexColor('#' + this.input);
    }
  }
}
</script>

<style>

</style>
