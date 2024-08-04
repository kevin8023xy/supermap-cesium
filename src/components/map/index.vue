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
    geocoder: true, // 是否显示位置查找工具
    homeButton: true, // 是否显示首页位置工具
    sceneModePicker: true, // 是否显示视角模式切换工具
    baseLayerPicker: true, // 是否显示默认图层选择工具
    navigationHelpButton: true, //是否显示导航帮助工具
    // 设置天空盒子
    skyBox: new Cesium.SkyBox({
      sources: {
        positiveX: "./Assets/Textures/SkyBox/px.jpg",
        negativeX: "./Assets/Textures/SkyBox/nx.jpg",
        positiveY: "./Assets/Textures/SkyBox/py.jpg",
        negativeY: "./Assets/Textures/SkyBox/ny.jpg",
        positiveZ: "./Assets/Textures/SkyBox/pz.jpg",
        negativeZ: "./Assets/Textures/SkyBox/nz.jpg",
      },
    }),
  });
  // 天地图矢量地图
  // viewer.imageryLayers.addImageryProvider(new Cesium.WebMapTileServiceImageryProvider({
  //   url: "http://t0.tianditu.com/vec_w/wmts?service=wmts&request=GetTile&version=1.0.0&LAYER=vec&tileMatrixSet=w&TileMatrix={TileMatrix}&TileRow={TileRow}&TileCol={TileCol}&style=default&format=tiles&tk="+tiandituKey,
  //   layer: "tdtVecBasicLayer",
  //   style: "default",
  //   format: "image/jpeg",
  //   tileMatrixSetID: "GoogleMapsCompatible",
  //   show: false
  // }));
  //
  // viewer.imageryLayers.addImageryProvider(new Cesium.WebMapTileServiceImageryProvider({
  //   url: "http://t0.tianditu.com/cva_w/wmts?service=wmts&request=GetTile&version=1.0.0&LAYER=cva&tileMatrixSet=w&TileMatrix={TileMatrix}&TileRow={TileRow}&TileCol={TileCol}&style=default.jpg&tk="+tiandituKey,
  //   layer: "tdtAnnoLayer",
  //   style: "default",
  //   format: "image/jpeg",
  //   tileMatrixSetID: "GoogleMapsCompatible"
  // }));

  // 天地图影像地图
  // viewer.imageryLayers.addImageryProvider(new Cesium.WebMapTileServiceImageryProvider({
  //   url: "http://t0.tianditu.com/img_w/wmts?service=wmts&request=GetTile&version=1.0.0&LAYER=img&tileMatrixSet=w&TileMatrix={TileMatrix}&TileRow={TileRow}&TileCol={TileCol}&style=default&format=tiles&tk="+tiandituKey,
  //   layer: "tdtBasicLayer",
  //   style: "default",
  //   format: "image/jpeg",
  //   tileMatrixSetID: "GoogleMapsCompatible",
  // }));

  // OSM地图
  // viewer.imageryLayers.addImageryProvider(
  //     new Cesium.UrlTemplateImageryProvider({
  //       url: 'https://tile-{s}.openstreetmap.fr/hot/{z}/{x}/{y}.png',
  //       subdomains: ["a", "b", "c", "d"],
  //     })
  // )

  // 高德矢量地图
  // viewer.imageryLayers.addImageryProvider(new Cesium.UrlTemplateImageryProvider({
  //   url: "http://webrd02.is.autonavi.com/appmaptile?lang=zh_cn&size=1&scale=1&style=8&x={x}&y={y}&z={z}",
  //   layer:'gdVectorLayer',
  //   minimumLevel: 4,
  //   maximumLevel: 18
  // }));

  // 地图叠加
  var imagerLayers = viewer.imageryLayers;
  var layer = imagerLayers.addImageryProvider(
    new Cesium.UrlTemplateImageryProvider({
      url: "http://webrd02.is.autonavi.com/appmaptile?lang=zh_cn&size=1&scale=1&style=8&x={x}&y={y}&z={z}",
      layer: "gdVectorLayer",
      minimumLevel: 4,
      maximumLevel: 18,
    }),
  );
  // 设置图层的透明度
  layer.alpha = 0.5;
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
