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
  const currentTop = Number(
    main?.style.top ? main?.style.top.slice(0, main?.style.top.length - 2) : 0
  );
  const width = main!.clientWidth;
  const height = main!.clientHeight;
  document.onmousemove = function (e) {
    const [endX, endY] = [e.clientX, e.clientY];
    if (direction.includes(DirectionState.LEFT)) {
      main && (main.style.left = `${currentLeft + endX - startX}` + "px");
      main && (main.style.width = `${width - (endX - startX) - 40}` + "px");
    }
    if (direction.includes(DirectionState.RIGHT)) {
      main && (main.style.width = `${width + (endX - startX) - 40}` + "px");
    }
    if (direction.includes(DirectionState.TOP)) {
      main && (main.style.top = `${currentTop + endY - startY}` + "px");
      main && (main.style.height = `${height - (endY - startY) - 40}` + "px");
    }
    if (direction.includes(DirectionState.BOTTOM)) {
      main && (main.style.height = `${height + (endY - startY) - 40}` + "px");
    }
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
      <p><slot/></p>
    </div>
  </div>
</template>

<style scoped>
@import url(./drag.css);
</style>
