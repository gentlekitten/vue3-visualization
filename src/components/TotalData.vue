<script setup>
import { onMounted, ref } from "vue";
import { CountUp } from "countup.js";
import { BorderBox1 as DvBorderBox1 } from "@kjgl77/datav-vue3";

const props = defineProps({
  data: {
    type: Object,
    required: true,
  },
});

const totalCountTarget = ref(null);
const cityOne = ref(null);
const cityTwo = ref(null);
const cityThree = ref(null);
const cityFour = ref(null);
const cityFive = ref(null);
const citySix = ref(null);

onMounted(() => {
  new CountUp(totalCountTarget.value, props.data.total).start();
  new CountUp(cityOne.value, props.data.hb).start();
  new CountUp(cityTwo.value, props.data.db).start();
  new CountUp(cityThree.value, props.data.hd).start();
  new CountUp(cityFour.value, props.data.zn).start();
  new CountUp(cityFive.value, props.data.xn).start();
  new CountUp(citySix.value, props.data.xb).start();
});
</script>
<template>
  <div>
    <dv-border-box1 class="flex flex-col">
      <div class="text-slate-300 text-center">
        数据总量：
        <span
          ref="totalCountTarget"
          class="text-7xl ml-2 mr-2 font-bold font-[Electronic] text-gradient"
        >
          679,473,929
        </span>
        条记录
      </div>
      <div class="mt-3 flex flex-wrap">
        <div class="w-1/3 text-center text-slate-400 text-sm">
          华北：
          <span ref="cityOne" class="text-[#5DC5EF] text-3xl font-[Electronic]">
            8,778,988
          </span>
        </div>
        <div class="w-1/3 text-center text-slate-400 text-sm">
          东北：<span ref="cityTwo" class="text-[#5DC5EF] text-3xl font-[Electronic]"
            >8,778,988</span
          >
        </div>
        <div class="w-1/3 text-center text-slate-400 text-sm">
          华东：<span ref="cityThree" class="text-[#5DC5EF] text-3xl font-[Electronic]"
            >8,778,988</span
          >
        </div>
        <div class="w-1/3 text-center text-slate-400 text-sm">
          中南：<span ref="cityFour" class="text-[#5DC5EF] text-3xl font-[Electronic]"
            >8,778,988</span
          >
        </div>
        <div class="w-1/3 text-center text-slate-400 text-sm">
          西南：<span ref="cityFive" class="text-[#5DC5EF] text-3xl font-[Electronic]"
            >8,778,988</span
          >
        </div>
        <div class="w-1/3 text-center text-slate-400 text-sm">
          西北：<span ref="citySix" class="text-[#5DC5EF] text-3xl font-[Electronic]"
            >8,778,988</span
          >
        </div>
      </div>
    </dv-border-box1>
  </div>
</template>
<style scoped>
:deep(.border-box-content) {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
</style>
