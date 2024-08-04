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
  });

  // 隐藏Logo
  viewer.cesiumWidget.creditContainer.style.display = "none";
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

  // 1.屏幕坐标系： 二维的笛卡尔坐标系 ，Cartesian2 类型
  // 2.地理坐标系，WGS-84坐标系，Cartographic类型，纬度，高度
  // 3.笛卡尔空间直角坐标系，Cartesian3类型

  // 角度与弧度的转换
  let radians = Cesium.Math.toRadians(90); // 角度转弧度 90°是 pi / 2
  console.log("radians", radians);
  // 弧度转角度
  let degree = Cesium.Math.toDegrees(radians);
  console.log("degree", degree);

  // 将经纬度转为笛卡尔坐标
  var cartesian3 = Cesium.Cartesian3.fromDegrees(
    // 经度
    89.5,
    // 纬度
    20.4,
    // 高度
    100,
  );
  console.log("cartesian3", cartesian3);

  // 将笛卡尔坐标转为经纬度
  var cartographic = Cesium.Cartographic.fromCartesian(cartesian3);
  console.log("cartographic", cartographic);
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
