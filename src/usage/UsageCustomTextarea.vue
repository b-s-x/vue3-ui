<script setup lang="ts">
import CustomTextarea from '../components/CustomTextarea.vue';
const handleInput = value => console.log('fatality', value);
</script>

<template>
  <div class="box">
    <custom-textarea
      key="1"
      value=""
      class="super"
      type="number"
      placeholder="Enter your username"
      @input="handleInput"
    />
  </div>
</template>

<style>
.box {
  width: 300px;
}
</style>
