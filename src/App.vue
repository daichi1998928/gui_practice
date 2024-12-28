<script setup>
const handleDragStart = (event) => {
  // ドラッグするデータを設定
  event.dataTransfer.setData('text/plain', event.target.id);
}

const handleDragOver = (event) => {
  // デフォルトのドラッグオーバー動作を防ぐ
  event.preventDefault();
}

const handleDrop = (event) => {
  // デフォルトのドロップ動作を防ぐ
  event.preventDefault();
  
  // ドロップ位置を取得
  const x = event.clientX;
  const y = event.clientY;
  
  // 要素の位置を更新
  const container = event.target;
  container.style.position = 'absolute';
  container.style.left = `${x}px`;
  container.style.top = `${y}px`;
}
</script>

<template>
  <div 
    class="container" 
    draggable="true"
    @touchstart="handleDragStart"
    @touchmove="handleDragOver"
    @touchend="handleDrop"
  >
  </div>
</template>

<style scoped>
.container {
  width: 250px;
  height: 250px;
  background-color: black;
  cursor: move; /* ドラッグ可能なことを示すカーソルを表示 */
}
</style>
