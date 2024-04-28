<template>
  <div id="map"></div>
</template>

<script setup>
import { onMounted, ref } from 'vue';

const map = ref(null);  // 使用 ref 来处理响应式数据

// 地图初始化方法
const initMap = () => {
  const leafletMap = L.map('map', {
    center: [24.485666, 118.095498], // 中心位置
    zoom: 12,  // 缩放级别
    minZoom: 3,
    maxZoom: 17,
    attributionControl: false,  // 版权控件
    zoomControl: true  // 缩放控件
  });

  map.value = leafletMap;  // 使用 ref 赋值
  L.tileLayer(
    "http://wprd04.is.autonavi.com/appmaptile?lang=zh_cn&size=1&style=7&x={x}&y={y}&z={z}"
  ).addTo(leafletMap);  // 加载底图
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
