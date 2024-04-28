<template>
  <div id="map"></div>
</template>

<script setup>
import { onMounted, onUnmounted, ref } from 'vue';

const map = ref(null);  // 使用 ref 来处理响应式数据

// 初始化地图
const initMap = () => {
  const leafletMap = L.map('map', {
    center: [34.210300073739916, 117.13945080254362],
    zoom: 17,
    minZoom: 3,
    maxZoom: 19,
    attributionControl: false,
    zoomControl: true
  });

  L.tileLayer(
    "http://wprd04.is.autonavi.com/appmaptile?lang=zh_cn&size=1&style=7&x={x}&y={y}&z={z}"
  ).addTo(leafletMap);

  const marker = L.marker([34.210300073739916, 117.13945080254362])
    .addTo(leafletMap)
    .bindPopup("<h1>hello</h1><button>hello world</button>");

  const circle = L.circle([34.215, 117.145], {
    color: 'red',
    fillColor: '#f03',
    fillOpacity: 0.3,
    radius: 800
  })
    .addTo(leafletMap)
    .bindPopup("<h1>hello</h1><button>hello world</button>");

  const popup = L.popup();

  // 地图点击事件处理器
  const onMapClick = (e) => {
    popup
      .setLatLng(e.latlng)
      .setContent("You clicked the map at " + e.latlng.toString())
      .openOn(leafletMap);
  };

  leafletMap.on('click', onMapClick);

  map.value = leafletMap;  // 存储地图实例
};

// 使用 onMounted 生命周期钩子来初始化地图
onMounted(initMap);

// 在组件销毁时销毁地图以避免内存泄漏
onUnmounted(() => {
  if (map.value) {
    map.value.remove();
  }
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
