<script setup>
import HorizontalBar from "./components/HorizontalBar.vue";
import MapChart from "./components/MapChart.vue";
import RadarBar from "./components/RadarBar.vue";
import Relation from "./components/Relation.vue";
import RingBar from "./components/RingBar.vue";
import TotalData from "./components/TotalData.vue";
import VerticalBar from "./components/VerticalBar.vue";
import WordCloud from "./components/WordCloud.vue";

import { getVisualization } from "@/api/visualization";
import { onMounted, ref } from "vue";

onMounted(() => {
  loadData();
});

const data = ref(null);

const loadData = async () => {
  const res = await getVisualization();
  data.value = res;
};

setInterval(() => {
  loadData();
}, 3000);
</script>

<template>
  <div
    v-if="data"
    class="bg-[url('./assets/image/bg.jpg')] min-w-min bg-cover bg-center h-screen text-white overflow-hidden pt-2 pb-2 pl-2 pr-1 flex"
  >
    <div class="flex-1 mr-3 p-3 flex flex-col">
      <!-- 横向柱状图 -->
      <HorizontalBar :data="data.regionData" class="h-1/3 box-border pb-2" />
      <!-- 雷达图 -->
      <RadarBar :data="data.riskData" class="h-1/3 box-border pb-2" />
      <!-- 关系图 -->
      <Relation :data="data.relationData" class="h-1/3" />
    </div>
    <div class="w-1/2 min-w-min mr-3 flex flex-col">
      <!-- 数据总览图 -->
      <TotalData :data="data.totalData" class="h-1/4" />
      <!-- 地图可视化 -->
      <MapChart :data="data.mapData" class="bg-opacity-70 bg-slate-800 mt-2 flex-1" />
    </div>
    <div class="flex-1 p-3 flex flex-col">
      <!-- 竖向柱状图 -->
      <VerticalBar :data="data.serverData" class="h-1/3 box-border pb-2" />
      <!-- 环形图 -->
      <RingBar :data="data.abnormalData" class="h-1/3 box-border pb-2" />
      <!-- 文档云图 -->
      <WordCloud :data="data.wordCloudData" class="h-1/3 box-border" />
    </div>
  </div>
</template>

<style scoped></style>
