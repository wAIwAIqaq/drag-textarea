<script setup lang="ts">
import DragTextarea from './components/DragTextarea.vue'
</script>

<template>
  <DragTextarea :drag-pos="true">
    我是跟随盒子宽度变化的font-size的文字
  </DragTextarea>
</template>

<style>
body{
  padding: 20px;
  margin: 0;
  display: flex;
  align-items: center;
  justify-content: center;
}
</style>
