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
      type: "value",
      // 不显示轴
      show: false,
      // 最大值
      max: function (value) {
        return parseInt(value.max * 1.2);
      },
    },
    yAxis: {
      type: "category",
      data: props.data.regions.map((item) => item.name),
      // 反向展示
      inverse: true,
      // 不展示轴线
      axisLine: {
        show: false,
      },
      // 不显示刻度
      axisTick: {
        show: false,
      },
      // 文字颜色
      axisLabel: {
        color: "#9EB1C8",
      },
    },
    grid: {
      top: 0,
      left: 0,
      bottom: 0,
      right: 0,
      // 计算边距时包含标签
      containLabel: true,
    },
    // 柱形图核心配置
    series: [
      {
        // 图表类型
        type: "bar",
        // 数据筛选
        data: props.data.regions.map((item) => ({
          name: item.name,
          value: item.value,
        })),
        // 显示背景
        showBackground: true,
        // 背景色
        backgroundStyle: {
          color: "rgba(180, 180, 180, 0.2)",
        },
        // 每个轴的样式
        itemStyle: {
          color: "#479AD3", // 设置柱子的颜色
          barBorderRadius: 5, // 设置柱子的圆角
          shadowColor: "rgba(0, 0, 0, 0.3)", // 设置柱子的阴影颜色
          shadowBlur: 5, // 设置柱子的阴影模糊大小
        },
        // 轴宽度
        barWidth: 12,
        // 轴上的字体
        label: {
          show: true,
          // 设置标签位置为右侧
          position: "right",
          textStyle: {
            // 设置标签文本颜色
            color: "#fff",
          },
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
    <dv-border-box11 class="pt-12" title="大区数据信息" :title-width="200">
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
