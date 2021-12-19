<script setup lang="ts">
import CustomTitle from '../components/CustomTitle.vue';
</script>

<template>
  <custom-title
    key="1"
    level="7"
    required
  >
    <span>bsx</span>
    <template #sub>
      mars
    </template>
  </custom-title>
</template>

<style>
</style>
