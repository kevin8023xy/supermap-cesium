<script setup lang="ts">
import * as Cesium from "cesium";
import { onMounted } from "vue";
import { ceisumToken, tiandituKey } from "@/utils/map/mapInfo.ts";
// 导入cesium静态资源
// import '@/assets/Widgets/widgets.css'

// 设置Cesium静态资源路径
// window.CESIUM_BASE_URL = '/'

// 设置cesium相机默认视角
Cesium.Camera.DEFAULT_VIEW_RECTANGLE = Cesium.Rectangle.fromDegrees(
  // 西边的经度
  89.5,
  // 南边的纬度
  20.4,
  // 东边经度
  110.4,
  61.2,
);
onMounted(() => {
  Cesium.Ion.defaultAccessToken = ceisumToken;
  const viewer = new Cesium.Viewer("cesiumContainer", {
    infoBox: false,
    geocoder: false, // 是否显示位置查找工具
    homeButton: true, // 是否显示首页位置工具
    sceneModePicker: true, // 是否显示视角模式切换工具
    baseLayerPicker: true, // 是否显示默认图层选择工具
    navigationHelpButton: false, //是否显示导航帮助工具
    timeline: false,
    // terrainProvider: new Cesium.CesiumTerrainProvider({
    //   url: "http://192.168.40.11:8090/iserver/services/3D-WeiHeLiuYuDOM/rest/realspace/datas/T4%E6%9D%8E%E5%AE%B6%E6%BB%A9%E2%80%94%E5%92%B8%E9%98%B3%E5%B8%82%E5%8C%BA%40DataSource2_17dom",
    // }),
  });

  var imageryProvider = new Cesium.UrlTemplateImageryProvider({
    url: "http://192.168.40.11:8090/iserver/services/3D-WeiHeLiuYuDOM/rest/realspace/datas/T4%E6%9D%8E%E5%AE%B6%E6%BB%A9%E2%80%94%E5%92%B8%E9%98%B3%E5%B8%82%E5%8C%BA%40DataSource2_17dom",
  });

  viewer.imageryLayers.addImageryProvider(imageryProvider);

  // 隐藏Logo
  // viewer.cesiumWidget.creditContainer.style.display = "none";
});
</script>

<template>
  <div class="map-box" id="cesiumContainer" ref="cesiumContainer"></div>
</template>

<style scoped>
.map-box {
  height: 100%;
  width: 100%;
}
</style>
