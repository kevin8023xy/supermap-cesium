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
  viewer.camera.setView({
    // 指定相机位置
    destination: guangzhoutaPosition,
    // 指定相机的朝向
    orientation: {
      heading: Cesium.Math.toRadians(0),
      pitch: Cesium.Math.toRadians(-90),
      // 指定相机的滚转角
      roll: 0,
    },
  });
  // 添加3D建筑
  // const osmBuildings = viewer.scene.primitives.add(
  //   new Cesium.createOsmBuildings(),
  // );
  async function addOsmBuildings() {
    try {
      const tileset = await Cesium.createOsmBuildingsAsync();
      viewer.scene.primitives.add(tileset);
    } catch (error) {
      console.log(`Error creating tileset: ${error}`);
    }
  }
  addOsmBuildings();
  // 创建一个点
  let point = viewer.entities.add({
    // 定位点的坐标
    position: guangzhoutaPointPosition,
    // 定位点的图标
    // billboard: {
    //   // 图标的url
    //   image: "./static/images/point.png",
    //   // 图标的大小
    //   width: 30,
    //   height: 30,
    // },

    // 点
    point: {
      pixelSize: 10,
      color: Cesium.Color.RED,
      outlineColor: Cesium.Color.WHITE,
      outlineWidth: 4,
    },
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
