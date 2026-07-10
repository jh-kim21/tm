<script setup>
import DefectGuide from './views/DefectGuide.vue'
</script>

<template>
  <DefectGuide />
</template>

<style>
*, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

body {
  font-family: 'Noto Sans KR', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
  background: #eef1f7;
  color: #2c3345;
  font-size: 12px;
  line-height: 1.4;
}

::-webkit-scrollbar { width: 5px; height: 5px; }
::-webkit-scrollbar-track { background: #f0f0f0; }
::-webkit-scrollbar-thumb { background: #c0c8d8; border-radius: 3px; }
</style>
