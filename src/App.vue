<script lang="ts" setup>
import KeenSlider from "./components/KeenSlider.vue";
import RangeSlider from "./components/rangeSlider.vue";

</script>
<template>
 
  <div class="bg-black">
    <div class="bg-red-600 ">
      <div class="relative h-40">
      <input type="range" oriented="vertical"  :value="70" class="absolute bottom-36" />
      <RangeSlider/>
    </div>
    </div>
    <KeenSlider class="mt-40" />
  </div>
</template>

<style scoped>
/*Chrome*/
input[type="range"] {
    -webkit-appearance: none;
    background: #C5CBD7 ;
    outline: none;
    transition: opacity 0.2s;
 height: 10px;
    border-radius: 4px;
    transform-origin: left;
    transform:rotate(-90deg);
  }
  input[type="range"]::-webkit-slider-thumb {
    -webkit-appearance: none;
    appearance: none;
    width: 20px;
    height: 20px;
    background: #3c67ff;
    border-radius: 100%;
    cursor: pointer;

  }

  input[type="range"]::-moz-range-thumb {
    width: 20px;
    height: 20px;
    background: #3c67ff;
    border-radius: 100%;
    cursor: pointer;
  }

</style>
