<script lang="ts">
import { ref, onMounted } from 'vue';
import * as echarts from 'echarts';
import { px } from '../common/px';
import { createEchartsOptions } from '../common/create-echarts-options';

export default {
    setup() {
        const divRef = ref(null);

        onMounted(() => {
            let myChart = echarts.init(divRef.value);
            myChart.setOption(
                createEchartsOptions({
                    legend: {
                        bottom: px(10),
                        textStyle: { color: 'white' },
                        itemWidth: px(30),
                        itemHeight: px(16),
                    },
                    grid: {
                        x: px(20),
                        x2: px(20),
                        y: px(20),
                        y2: px(70),
                        containLabel: true,
                    },
                    xAxis: {
                        type: 'category',
                        boundaryGap: false,
                        data: [2015, 2016, 2017, 2018, 2019, 2020, 2021, 2022],
                        splitLine: { show: true, lineStyle: { color: '#073E78' } },
                        axisTick: { show: false },
                        axisLine: { show: false },
                    },
                    yAxis: {
                        type: 'value',
                        splitLine: { lineStyle: { color: '#073E78' } },
                        axisLabel: {
                            formatter(val) {
                                return val * 100 + '%';
                            },
                        },
                    },
                    series: [
                        {
                            name: '抢劫',
                            type: 'line',
                            data: [0.01, 0.02, 0.03, 0.04, 0.05, 0.06, 0.07, 0.08, 0.09].reverse(),
                        },
                        {
                            name: '醉驾',
                            type: 'line',
                            data: [0.02, 0.03, 0.04, 0.05, 0.06, 0.07, 0.08, 0.09, 0.1].reverse(),
                        },
                        {
                            name: '盗窃',
                            type: 'line',
                            data: [0.03, 0.04, 0.05, 0.06, 0.07, 0.08, 0.09, 0.1, 0.11].reverse(),
                        },
                        {
                            name: '故意杀人',
                            type: 'line',
                            data: [0.04, 0.05, 0.06, 0.07, 0.08, 0.09, 0.1, 0.11, 0.12].reverse(),
                        },
                        {
                            name: '故意伤人',
                            type: 'line',
                            data: [0.05, 0.06, 0.07, 0.08, 0.09, 0.1, 0.11, 0.12, 0.13].reverse(),
                        },
                    ].map((obj) => ({
                        ...obj,
                        symbol: 'circle',
                        symbolSize: px(12),
                        lineStyle: { width: px(2) },
                    })),
                })
            );
        });

        return {
            divRef,
        };
    },
};
</script>

<template>
    <div class="bordered faanqushi">
        <h2>发案趋势分析</h2>
        <div ref="divRef" class="chart" />
    </div>
</template>
