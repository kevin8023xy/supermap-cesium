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
  viewer.camera.setView({
    // 指定相机位置
    destination: position,
    // 指定相机的朝向
    orientation: {
      heading: Cesium.Math.toRadians(0),
      pitch: Cesium.Math.toRadians(-20),
      // 指定相机的滚转角
      roll: 0,
    },
  });
  // 通过方向键移动相机
  document.addEventListener("keydown", (e) => {
    // 获取相机离地面高度
    let height = viewer.camera.positionCartographic.height;
    let moveRate = height / 100;
    if (e.key === "w") {
      // 设置向前移动
      viewer.camera.moveForward(moveRate);
    } else if (e.key === "s") {
      // 设置向后移动
      viewer.camera.moveBackward(moveRate);
    } else if (e.key === "a") {
      viewer.camera.moveLeft(moveRate);
    } else if (e.key === "d") {
      viewer.camera.moveRight(moveRate);
    } else if (e.key === "q") {
      // 设置相机向左旋转
      viewer.camera.lookLeft(Cesium.Math.toRadians(0.1));
    } else if (e.key === "e") {
      viewer.camera.lookRight(Cesium.Math.toRadians(0.1));
    } else if (e.key === "r") {
      // 设置向上旋转相机
      viewer.camera.lookUp(Cesium.Math.toRadians(0.1));
    } else if (e.key === "f") {
      // 设置向上旋转相机
      viewer.camera.lookDown(Cesium.Math.toRadians(0.1));
    } else if (e.key === "g") {
      // 向左逆时针翻滚
      viewer.camera.twistLeft(Cesium.Math.toRadians(0.1));
    } else if (e.key === "h") {
      // 向右逆时针翻滚
      viewer.camera.twistRight(Cesium.Math.toRadians(0.1));
    }
  });
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
