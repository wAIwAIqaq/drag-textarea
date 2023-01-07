<script setup lang="ts">
import { DirectionState } from "./enums";
function resizeHandler(e: any) {
  //   const resize = <any>e.target;
  //   const left = e.target.parentNode;
  //   // var lfex = document.getElementsByClassName("mid");
  //   const box = e.target?.parentNode.parentNode;
  //   const right = box.children[1];
  //   // 鼠标按下事件
  //   resize.onmousedown = function (e: any) {
  //     const startX = e.clientX;
  //     resize.left = resize.offsetLeft;
  //     document.onmousemove = function (e) {
  //       const endX = e.clientX;
  //       console.log(startX, endX);
  //       const flexRatio = (resize.left + (endX - startX)) / (right.clientWidth);
  //       if(flexRatio > 2 || flexRatio < 0.5) return;
  //       left.style.flex = flexRatio;
  //     };
  //     document.onmouseup = function (e) {
  //       document.onmousemove = null;
  //       document.onmouseup = null;
  //       resize.releaseCapture && resize.releaseCapture();
  //     };
  //     resize.setCapture && resize.setCapture();
  //     return false;
  //   };
  const direction = e.target.id;
  console.log(direction);
}
function reposHandler(e: any) {
  console.log(e.target);
}
</script>
<template>
  <div class="d-container">
    <div class="d-main">
      <div
        class="d-slider__top"
        :id="DirectionState.TOP"
        @mousedown="resizeHandler"
      />
      <div
        class="d-slider__right"
        :id="DirectionState.RIGHT"
        @mousedown="resizeHandler"
      />
      <div
        class="d-slider__left"
        :id="DirectionState.LEFT"
        @mousedown="resizeHandler"
      />
      <div
        class="d-slider__bottom"
        :id="DirectionState.BOTTOM"
        @mousedown="resizeHandler"
      />
      <div
        class="d-slider__top-left"
        :id="DirectionState.TOP_LEFT"
        @mousedown="resizeHandler"
      />
      <div
        class="d-slider__top-right"
        :id="DirectionState.TOP_RIGHT"
        @mousedown="resizeHandler"
      />
      <div
        class="d-slider__bottom-right"
        :id="DirectionState.BOTTOM_RIGHT"
        @mousedown="resizeHandler"
      />
      <div
        class="d-slider__bottom-left"
        :id="DirectionState.BOTTOM_LEFT"
        @mousedown="resizeHandler"
      />
      <span class="d-slider__move" @mousedown="reposHandler"></span>
      <p>111</p>
    </div>
  </div>
</template>

<style scoped>
.d-container {
  position: relative;
  min-width: 200px;
  width: 200px;
  height: 200px;
  min-height: 200px;
  margin: 10px;
  border: 1px solid red;
  border-radius: 5px;
}
.d-main {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  padding: 20px;
}
.d-slider__top,
.d-slider__bottom {
  cursor: row-resize;
}
.d-slider__left,
.d-slider__right {
  cursor: col-resize;
}
.d-slider__top {
  position: absolute;
  left: 5px;
  right: 5px;
  top: -5px;
  height: 10px;
  background: blue;
}
.d-slider__right {
  position: absolute;
  top: 5px;
  bottom: 5px;
  right: -5px;
  width: 10px;
  background: blue;
}
.d-slider__bottom {
  position: absolute;
  left: 5px;
  right: 5px;
  bottom: -5px;
  height: 10px;
  background: blue;
}
.d-slider__left {
  position: absolute;
  top: 5px;
  bottom: 5px;
  left: -5px;
  width: 10px;
  background: blue;
}
.d-slider__top-left {
  background: aqua;
  position: absolute;
  top: -5px;
  left: -5px;
  height: 10px;
  width: 10px;
  cursor: nw-resize;
}

.d-slider__top-right {
  background: aqua;
  position: absolute;
  top: -5px;
  right: -5px;
  height: 10px;
  width: 10px;
  cursor: ne-resize;
}

.d-slider__bottom-right {
  background: aqua;
  position: absolute;
  bottom: -5px;
  right: -5px;
  height: 10px;
  width: 10px;
  cursor: se-resize;
}

.d-slider__bottom-left {
  background: aqua;
  position: absolute;
  bottom: -5px;
  left: -5px;
  height: 10px;
  width: 10px;
  cursor: sw-resize;
}
.d-slider__move {
  position: absolute;
  cursor: move;
  width: 10px;
  height: 10px;
  left: 50%;
  transform: translateX(-50%);
  border-radius: 50%;
  background: aqua;
  bottom: -20px;
}
p {
  margin: 0;
}
</style>
