<template>
  <div id="app">
    <div class="slider">
      <div class="slider-value">{{ Math.round(value) }}</div>
      <div class="slider-hit-area" @click="onClick">
        <div class="slider-container" ref="container">
          <div class="filled" :style="{ height: value + '%' }"></div>
          <div
            class="handle"
            :style="{ bottom: value + '%' }"
            @mousedown="onMouseDown"
          ></div>
        </div>
      </div>
    </div>
  </div>
</template>

<script lang="ts" setup>
import { onMounted, ref } from "vue";


const value = ref(30);
const dragging = ref(false);
const container = ref();

function onMouseDown() {
  dragging.value = true;
}
function clamp(val: any, min: any, max: any) {
  return Math.max(min, Math.min(max, val));
}
function getRect() {
  return container.value.getBoundingClientRect();
}
function update(e) {
  const rect = getRect();
  value.value =
    100 -
    ((clamp(e.clientY, rect.top, rect.bottom) - rect.top) / rect.height) * 100;
}
function onClick(e) {
  update(e);
}
onMounted(() => {
  document.addEventListener("mousemove", (e) => {
    if (!dragging.value) return;
    update(e);
  });
  document.addEventListener("mouseup", (e) => {
    dragging.value = false;
  });
});
</script>
<style lang="scss">
.slider {
  background-color: #f4f4f4;
  padding: 1em 0;
  width: 2.6em;
  border-radius: 0.25em;
  .slider-value {
    text-align: center;
    width: 100%;
    margin-bottom: 1em;
    font-family: sans-serif;
  }
  .slider-hit-area {
    height: 10em;
    width: 100%;
    cursor: pointer;
    display: flex;
    flex-direction: column;
    align-items: center;

    .slider-container {
      width: 3px;
      height: 100%;
      background-color: #ddd;
      position: relative;
      .filled {
        background-color: red;
        width: 100%;
        position: absolute;
        bottom: 0;
        left: 0;
      }
      .handle {
        width: 1em;
        height: 1em;
        border-radius: 100%;
        background-color: red;
        position: absolute;
        left: 50%;
        transform: translate(-50%, 50%);
      }
    }
  }
}
</style>
