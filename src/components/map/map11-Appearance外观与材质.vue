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

  // setView 瞬间到达指定位置，视角
  let position = Cesium.Cartesian3.fromDegrees(116.397428, 39.90923, 1000);
  // 广州塔的位置
  let guangzhoutaPosition = Cesium.Cartesian3.fromDegrees(
    113.3191,
    23.109,
    1000,
  );
  let guangzhoutaPointPosition = Cesium.Cartesian3.fromDegrees(
    113.3191,
    23.109,
    500,
  );
  let newPosition = Cesium.Cartesian3.fromDegrees(135, 20, 10000000);
  viewer.camera.setView({
    // 指定相机位置
    destination: newPosition,
    // 指定相机的朝向
    orientation: {
      heading: Cesium.Math.toRadians(0),
      pitch: Cesium.Math.toRadians(-90),
      // 指定相机的滚转角
      roll: 0,
    },
  });
  // 01-创建几何
  const rectangele = new Cesium.RectangleGeometry({
    ellipsoid: Cesium.Ellipsoid.WGS84,
    rectangle: Cesium.Rectangle.fromDegrees(
      115, // 西边经度
      20, // 南边纬度
      135, // 东边经度
      30, // 北边纬度
    ),
    // 距离表面高度
    height: 0,
    vertexFormat: Cesium.PerInstanceColorAppearance.VERTEX_FORMAT, // 这个是
  });

  const rectangele2 = new Cesium.RectangleGeometry({
    ellipsoid: Cesium.Ellipsoid.WGS84,
    rectangle: Cesium.Rectangle.fromDegrees(
      140, // 西边经度
      20, // 南边纬度
      160, // 东边经度
      30, // 北边纬度
    ),
    // 距离表面高度
    height: 0,
    vertexFormat: Cesium.PerInstanceColorAppearance.VERTEX_FORMAT, // 这个是
  });

  // 02-创建几何体实例
  let instance = new Cesium.GeometryInstance({
    geometry: rectangele,
    attributes: {
      color: Cesium.ColorGeometryInstanceAttribute.fromColor(
        Cesium.Color.RED.withAlpha(0.5),
      ),
    },
  });
  let instance2 = new Cesium.GeometryInstance({
    id: "blueRect",
    geometry: rectangele2,
    attributes: {
      color: Cesium.ColorGeometryInstanceAttribute.fromColor(
        Cesium.Color.BLUE.withAlpha(0.5),
      ),
    },
  });
  // material
  let material1: any = new Cesium.Material.fromType("Color", {
    color: Cesium.Color.AQUA.withAlpha(0.5),
  });
  // 03-设置外观
  // let appearance = new Cesium.PerInstanceColorAppearance({
  //   material: material1,
  // });

  let appearance = new Cesium.MaterialAppearance({
    material: material1,
  });
  // 04-图元
  let primitive = new Cesium.Primitive({
    geometryInstances: [instance, instance2],
    appearance: appearance,
  });
  // 05-添加到viewer
  viewer.scene.primitives.add(primitive);
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
