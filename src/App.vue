<template>
  <div id="app">
    <h1>White PNG Color shift</h1>
    <div>
      <h2>Desired color format</h2>
      <color-type-selector @typeSelected="onTypeSelected" 
        :type="type">
      </color-type-selector>
    </div>
    <div>
      <hex-color-input v-if="type === namespaces.HEX"
        @hexInput="onHexInput">
      </hex-color-input>
      <r-g-b-color-input v-else
        @rgbInput="onRgbInput">
      </r-g-b-color-input>

      <button :disabled="!rgbColorTarget">GENERATE FILTER</button>
    </div>
    
  </div>
</template>

<script>
import * as namespaces from './namespaces/colorsType';
import { hexToRgb } from './utils/colorUtils.js';

import ColorTypeSelector from './components/ColorTypeSelector';
import HexColorInput from './components/HexColorInput';
import RGBColorInput from './components/RGBColorInput';

export default {
  name: 'app',
  components: {
    ColorTypeSelector,
    HexColorInput,
    RGBColorInput
  },
  data: function() {
    return {
      type: namespaces.HEX,
      namespaces: namespaces,
      rgbColorTarget: null
    } 
  },
  methods: {
    onTypeSelected(type) {
      this.type = type;
    },
    onHexInput(hexColor) {
      this.rgbColorTarget = hexToRgb(hexColor);
    },
    onRgbInput(rgb) {
      this.rgbColorTarget = rgb;
    }
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css?family=Lato');
#app {
  font-family: 'Lato', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

input, button {
   font-family: 'Lato', Helvetica, Arial, sans-serif;
}
</style>
