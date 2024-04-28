<template>
  <div id="map"></div>
</template>

<script setup>
import { onMounted, ref } from 'vue';

const map = ref(null);  // 使用 ref 来处理响应式数据

// 地图初始化方法
const initMap = () => {
  map.value = L.map('map', {
    center: [34.210300073739916, 117.13945080254362], // 中心位置
    zoom: 17,  // 缩放级别
    minZoom: 3,
    maxZoom: 19,
    attributionControl: false,  // 版权控件
    zoomControl: true  // 缩放控件
  });

  // map.value = leafletMap;  // 使用 ref 赋值
  L.tileLayer(
    "http://wprd04.is.autonavi.com/appmaptile?lang=zh_cn&size=1&style=7&x={x}&y={y}&z={z}"
  ).addTo(map.value);  // 加载底图
};

// 使用 onMounted 生命周期钩子来初始化地图
onMounted(() => {
  initMap();
});

</script>

<style scoped>
#map {
  width: 100vw;
  height: 100vh;
  position: absolute;
  top: 0;
  left: 0;
}
</style>
