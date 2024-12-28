<script setup>
import { ref } from 'vue';

const position = ref({ x: 0, y: 0 });
let isDragging = ref(false);

const handleDragStart = (event) => {
  isDragging.value = true;
}

const handleDragOver = (event) => {
  event.preventDefault();
}

const handleDrop = (event) => {
  console.log('handleDrop');
  isDragging.value = false;
  position.value = {
    x: event.clientX,
    y: event.clientY
  };
  console.log(position.value);
}

const handleTouchStart = (event) => {
  isDragging.value = true;
}

const handleTouchMove = (event) => {
  if (isDragging.value) {
    event.preventDefault();
    const touch = event.touches[0];
    position.value = {
      x: touch.clientX,
      y: touch.clientY
    };
  }
}

const handleTouchEnd = () => {
  isDragging.value = false;
}
</script>

<template>
  <div 
    class="drop-area"
    @dragover="handleDragOver"
    @drop="handleDrop"
  >
    <div 
      class="container" 
      draggable="true"
      @dragstart="handleDragStart"
      @touchstart="handleTouchStart"
      @touchmove="handleTouchMove"
      @touchend="handleTouchEnd"
      :style="{
        position: 'absolute',
        left: `${position.x}px`,
        top: `${position.y}px`
      }"
    >
    </div>
  </div>
</template>

<style scoped>
.drop-area {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100vh;
  z-index: 1;
}

.container {
  width: 250px;
  height: 250px;
  background-color: black;
  cursor: move;
  touch-action: none;
  z-index: 2;
}
</style>