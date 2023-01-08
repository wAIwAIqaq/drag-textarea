<script setup lang="ts">
import { DirectionState } from "./enums";
import { defineProps } from "vue";
const props = defineProps(["dragPos"]);
const { dragPos } = props;
function resizeHandler(e: any) {
  const direction = e.target.id;
  console.log(direction);
  const slider = e.target;
  const main = document.getElementById("main");
  const [startX, startY] = [e.clientX, e.clientY];
  const currentLeft = Number(
    main?.style.left
      ? main?.style.left.slice(0, main?.style.left.length - 2)
      : 0
  );
  const width = main!.clientWidth;
  console.log(width, main?.style);
  const currentTop = Number(
    main?.style.top ? main?.style.top.slice(0, main?.style.top.length - 2) : 0
  );
  document.onmousemove = function (e) {
    const [endX, endY] = [e.clientX, e.clientY];
    main && (main.style.left = `${currentLeft + endX - startX}` + "px");
    main && (main.style.width = `${width - (endX - startX) - 40}` + "px");
    console.log(`${width - (endX - startX)} + 'px'`);
  };
  document.onmouseup = function (e) {
    document.onmousemove = null;
    document.onmouseup = null;
    slider.releaseCapture && slider.releaseCapture();
  };
  slider.setCapture && slider.setCapture();
  return false;
}

function reposHandler(e: any) {
  if (!dragPos) return;
  const icon = e.target;
  const main = document.getElementById("main");
  const [startX, startY] = [e.clientX, e.clientY];
  const currentLeft = Number(
    main?.style.left
      ? main?.style.left.slice(0, main?.style.left.length - 2)
      : 0
  );
  const currentTop = Number(
    main?.style.top ? main?.style.top.slice(0, main?.style.top.length - 2) : 0
  );
  console.log(currentLeft, currentTop);
  document.onmousemove = function (e) {
    const [endX, endY] = [e.clientX, e.clientY];
    main && (main.style.left = `${currentLeft + endX - startX}` + "px");
    main && (main.style.top = `${currentTop + endY - startY}` + "px");
  };
  document.onmouseup = function (e) {
    document.onmousemove = null;
    document.onmouseup = null;
    icon.releaseCapture && icon.releaseCapture();
  };
  icon.setCapture && icon.setCapture();
  return false;
}
</script>
<template>
  <div class="d-container" :class="{ 'is-relative': dragPos }">
    <div class="d-main" id="main">
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
      <span
        v-if="dragPos"
        class="d-slider__move"
        @mousedown="reposHandler"
      ></span>
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
}
.d-main {
  position: absolute;
  container-type: inline-size;
  margin: 10px;
  width: 100%;
  height: 100%;
  border: 1px solid red;
  border-radius: 5px;
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
  font-size: calc(100cqw / 20);
}
</style>
