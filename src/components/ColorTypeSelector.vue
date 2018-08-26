<template>
  <div class="color-type-selectors">
    <input type="radio" 
      :value="namespaces.HEX"
      :id="namespaces.HEX"
      @change="onTypeSelect"
      v-model="selectedType">
    <label :for="namespaces.HEX" 
      class="color-type-selectors-label">
      {{namespaces.HEX}}
    </label>
    <input type="radio" 
      :value="namespaces.RGB"
      :id="namespaces.RGB"
      @change="onTypeSelect" 
      v-model="selectedType">
    <label :for="namespaces.RGB" 
      class="color-type-selectors-label">
      {{namespaces.RGB}}
    </label>
  </div>
</template>

<script>
import * as namespaces from '../namespaces/colorsType';

export default {
  props: ['type'],
  data: function() {
    return {
      namespaces: namespaces,
      selectedType: this.type
    }
  },
  methods: {
    onTypeSelect() {
      this.$emit('typeSelected', this.selectedType);
    }
  }
}
</script>

<style scoped>
  .color-type-selectors-label {
    text-transform: uppercase;
  }
</style>