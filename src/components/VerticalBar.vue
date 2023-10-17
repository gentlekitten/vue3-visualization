<script setup>
import { defineProps, ref, onMounted, watch } from "vue";
import * as echarts from "echarts";
import { BorderBox11 as DvBorderBox11 } from "@kjgl77/datav-vue3";

const props = defineProps({
  data: {
    type: Object,
    require: true,
  },
});

const target = ref(null);

let mChart = null;
onMounted(() => {
  mChart = echarts.init(target.value);
  renderChart();
});

const renderChart = () => {
  const options = {
    xAxis: {
      // 数据显示
      type: "category",
      data: props.data.servers.map((item) => item.name),
      // 文字色值
      axisLabel: {
        color: "#9EB1C8",
      },
    },
    yAxis: {
      // 数据展示
      type: "value",
      // 不显示轴
      show: false,
      // 最大值（防止触顶）
      max: function (value) {
        // 取整
        return parseInt(value.max * 1.2);
      },
    },
    grid: {
      top: 16,
      right: 0,
      bottom: 26,
      left: -26,
      // 计算边距时包含标签
      containLabel: true,
    },
    // 柱形图核心配置
    series: [
      {
        // 图表类型
        type: "bar",
        // 数据筛选
        data: props.data.servers.map((item) => ({
          name: item.name,
          value: item.value,
        })),
        // 每个轴的样式
        itemStyle: {
          color: "#479AD3", // 设置柱子的颜色
          barBorderRadius: [5, 5, 0, 0], // 设置柱子的圆角
          shadowColor: "rgba(0, 0, 0, 0.3)", // 设置柱子的阴影颜色
          shadowBlur: 5, // 设置柱子的阴影模糊大小
        },
        // 柱子宽度
        barWidth: 12,
        // 文本
        label: {
          show: true,
          // 设置标签位置为右侧
          position: "top",
          textStyle: {
            // 设置标签文本颜色
            color: "#fff",
          },
          formatter: "{c}%",
        },
      },
    ],
  };
  mChart.setOption(options);
};

watch(
  () => props.data,
  () => renderChart()
);
</script>
<template>
  <div>
    <dv-border-box11 class="pt-10" title="服务资源占用比" :title-width="200">
      <div ref="target" class="w-5/6 h-5/6"></div>
    </dv-border-box11>
  </div>
</template>
<style scoped>
:deep(.border-box-content) {
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>
