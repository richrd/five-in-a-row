<script setup lang="ts">
import { ref } from 'vue'
import Cell from './Cell.vue'

const boardState = ref([])
const boardSize = 100; // Width & Height
let lastPlacement = 1

const populateBoard = () => {
  let y = 0
  let x = 0
  while (y < boardSize) {
    boardState.value.push([])
    while (x < boardSize) {
      boardState.value[y].push({ id: `${x},${y}`, value: 0 })
      x += 1
    }
    x = 0
    y += 1
  }
}

const cellClick = (x, y) => {
  const cellValue = boardState.value[y][x].value
  if (cellValue) {
    boardState.value[y][x].value = 0
    return
  } else {
    boardState.value[y][x].value = lastPlacement == 1 ? 2 : 1
    lastPlacement = boardState.value[y][x].value
  }
}
const cellValueToSymbol = (value: number) => {
  // console.log("cellValueToSymbol", value);
  return [' ', 'X', 'O'][value]
}
populateBoard()
</script>

<style>
.row {
  display: flex;
}
</style>

<template>
  <div>
    <div v-for="(row, yIndex) in boardState" class="row" :key="yIndex">
      <div v-for="(cell, xIndex) in row" class="item" :key="cell.id" :title="cell.id">
        <Cell @click="cellClick(xIndex, yIndex)" class="square" :value="cell.value" />
        <!--<div @click="cellClick(xIndex, yIndex)" class="cell">{{ cellValueToSymbol(cell.value) }}</div>-->
      </div>
    </div>
  </div>
</template>
