<script setup lang="ts">
import { onMounted } from "vue";
import Map from "@/components/map/index.vue";
// 2
// 2.1坐标转换
import map坐标转换Vue from "@/components/map/map01-坐标转换.vue";
import map相机的方向和位置Vue from "@/components/map/map02-相机的方向和位置&交互.vue";
import map03添加物体与3D建筑物Vue from "./components/map/map03-添加物体与3D建筑物.vue";
import map04标签与广告牌Vue from "./components/map/map04-标签与广告牌.vue";
import map053D模型添加与设置Vue from "./components/map/map05-3D模型添加与设置.vue";
import map06创建primitive元素Vue from "./components/map/map06-创建primitive元素.vue";
import map07多个实体再同一个primitiveVue from "./components/map/map07-多个实体在同一个primitive.vue";
import map08Entity和primitive物体交互Vue from "./components/map/map08-entity和primitive物体交互.vue";
import map09Entity材质Vue from "./components/map/map09-entity材质.vue";
import map10Entity折线材质设置Vue from "./components/map/map10-entity折线材质设置.vue";
import map11Appearance外观与材质Vue from "./components/map/map11-Appearance外观与材质.vue";
import map12Primitive材质Vue from "./components/map/map12-primitive材质.vue";
import App05Vue from "./components/map/App05-添加地形.vue";

onMounted(() => {
  // Ceisum
});
</script>

<template>
  <div id="app-container">
    <!--   <Map  />-->
    <!--    <map坐标转换Vue />-->
    <!--    <map相机的方向和位置Vue />-->
    <!--    <map03添加物体与3D建筑物Vue />-->
    <!--    <map04标签与广告牌Vue />-->
    <!--    <map053D模型添加与设置Vue />-->
    <!--    <map06创建primitive元素Vue />-->
    <!--    <map07多个实体再同一个primitiveVue />-->
    <!--    <map08Entity和primitive物体交互Vue />-->
    <!--    <map09Entity材质Vue />-->
    <!--    <map10Entity折线材质设置Vue />-->
    <!--    <map11Appearance外观与材质Vue />-->
    <!--    <map12Primitive材质Vue />-->
    <App05Vue />
  </div>
</template>

<style scoped>
#app-container {
  width: 100%;
  height: 100%;
}
</style>
