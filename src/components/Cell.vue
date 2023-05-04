<template>
  <div class="cell" :data-value="props.value"></div>
</template>

<script setup lang="ts">
const props = defineProps(['value'])
</script>

<style>
.cell {
  width: 20px;
  height: 20px;
  border: 1px solid #333;
  display: flex;
  justify-content: center;
  align-items: center;
  cursor: crosshair;
  position: relative;
}

.cell:hover {
  background: #222;
  border: 1px solid salmon;
}

.cell[data-value='2']:after {
  content: '';
  display: inline-block;
  width: 55%;
  height: 55%;
  border: 1.5px solid #ddd;
  border-radius: 100%;
}

.cell[data-value='1']:before,
.cell[data-value='1']:after {
  position: absolute;
  content: '';
  display: inline-block;
  width: 82%;
  border-top: 1.5px solid #ddd;
  transform: rotate(45deg);
}
.cell[data-value='1']:before {
  transform: rotate(-45deg);
}
</style>
