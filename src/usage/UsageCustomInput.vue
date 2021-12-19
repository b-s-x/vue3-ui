<script setup lang="ts">
import CustomInput from '../components/CustomInput.vue';
const handlerInput = value => console.log('fatality', value);
const handlerKeydown = value => console.log('fatality2', value);
</script>

<template>
  <div class="title">
    <custom-input
      key="1"
      value="111"
      class="super"
      type="number"
      placeholder="Enter your username"
      @input="handlerInput"
      @keydown="handlerKeydown"
    />
    <custom-input
      key="1"
      value="111"
      class="super"
      type="number"
      placeholder="Enter your username"
      required
      @input="handlerInput"
      @keydown="handlerKeydown"
    />
  </div>
</template>

<style>
</style>
