<script setup lang="ts">
import CustomButton from '../components/CustomButton.vue';
const handlerClick = (event: Event) => console.log('fatality', event);
</script>

<template>
  <div class="title">
    <custom-button
      key="1"
      value="111"
      class="super"
      type="number"
      placeholder="Enter your username"
      @click="handlerClick"
    >
      111111
    </custom-button>
  </div>
</template>

<style>
</style>
