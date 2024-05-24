<template>
  <div class="p-20px">
    <div class="wrapper size-full">
      <div class="title">
        <div class="h-full flex-y-center gap-5px">
          <icon-local-year class="text-icon text-primary" />
          <span class="text-16px text-primary text-primary">年度情况</span>
        </div>
      </div>
      <div class="year">
        <TimeLine v-model="year" :option="timeOptions"></TimeLine>
      </div>
      <div class="select">
        <div class="size-full flex items-end justify-end">
          <n-tabs class="w-fit" size="large">
            <n-tab v-for="item in tabOptions" :key="item.value" :name="item.value">
              {{ item.label }}
            </n-tab>
          </n-tabs>
        </div>
      </div>
      <div class="statistics1">
        <div class="size-full flex gap-20px">
          <n-card
            v-for="(item, index) in statisticalItems"
            :key="index"
            :bordered="false"
            size="small"
            class="h-full justify-between rounded-0"
            :style="{ backgroundColor: mixColor(theme.themeColor, colors[index % colors.length], 0.7) }"
          >
            <template #header>
              <div>{{ item.type }}</div>
            </template>
            <template #header-extra>
              <div class="flex items-end">
                <p>{{ item.num }}</p>
                <span>{{ item.unit }}</span>
              </div>
            </template>
            <template #footer>
              <div class="flex items-end justify-between">
                <p>{{ item.county }}</p>
                <p>{{ item.dataTime }}</p>
              </div>
            </template>
          </n-card>
        </div>
      </div>
      <div class="statistics2">
        <div class="size-full flex gap-10px">
          <n-card
            v-for="(item, index) in 3"
            :key="index"
            :bordered="false"
            size="small"
            class="border-l-6 rounded-0 bg-transparent bg-gradient-to-r"
            :style="{
              backgroundImage: `linear-gradient(to right, ${mixColor(
                theme.themeColor,
                colors2[index % colors2.length],
                0.7
              )}40 , transparent)`,
              borderLeftColor: mixColor(theme.themeColor, colors2[index % colors2.length], 0.7)
            }"
          >
            <div class="h-full flex-center flex-col">
              <h1 class="" :style="{ color: mixColor(theme.themeColor, colors2[index % colors2.length], 0.7) }">
                第1代
              </h1>
              <div
                class="my-10px h-2px w-30px"
                :style="{ backgroundColor: mixColor(theme.themeColor, colors2[index % colors2.length], 0.7) }"
              ></div>
              <div class="mb-20px">04-16至05-20</div>
              <div class="flex-x-center gap-5px">
                <div class="flex-y-center flex-col">
                  <p class="mb-20px">--</p>
                  <span>平均捕虫量</span>
                  <span>（头）</span>
                </div>
                <n-divider vertical class="self-center !h-30px !-mt-10px" />
                <div class="flex-y-center flex-col">
                  <p class="mb-20px">--</p>
                  <span>平均捕虫量</span>
                  <span>（头）</span>
                </div>
                <n-divider vertical class="self-center !h-30px !-mt-10px" />
                <div class="flex-y-center flex-col">
                  <p class="mb-20px">--</p>
                  <span>平均捕虫量</span>
                  <span>（头）</span>
                </div>
              </div>
            </div>
          </n-card>
        </div>
      </div>
      <div class="chart1">
        <div class="h-full flex-vertical">
          <div class="mt-10px">
            <p>2023年时空走势图</p>
          </div>
          <div ref="chart1Ref" class="h-full"></div>
        </div>
      </div>
      <div class="right">
        <div class="chart2">
          <div class="h-full flex-vertical">
            <div class="flex-y-center gap-5px">
              <icon-local-weather class="text-icon text-primary" />
              <span class="text-16px text-primary text-primary">气象与虫情</span>
            </div>
            <div ref="chart2Ref" class="h-full"></div>
            <n-card
              :bordered="false"
              size="small"
              class="border-l-6 rounded-0 bg-transparent bg-gradient-to-r"
              :style="{
                backgroundImage: `linear-gradient(to right, ${mixColor(
                  theme.themeColor,
                  colors2[0],
                  0.7
                )}40 , transparent)`,
                borderLeftColor: mixColor(theme.themeColor, colors2[0], 0.7)
              }"
            >
              <template #header>
                <div :style="{ color: mixColor(theme.themeColor, colors2[0], 0.7) }">常年平均情况</div>
              </template>
              <div class="flex-x-center gap-25px">
                <div class="flex-y-center flex-col">
                  <p class="mb-5px text-16px">
                    62.9
                    <span class="text-12px">天</span>
                  </p>
                  <span>发生天数</span>
                  <span>第一代</span>
                </div>
                <n-divider vertical class="self-center !h-30px !-mt-10px" />
                <div class="flex-y-center flex-col">
                  <p class="mb-5px text-16px">
                    180.4
                    <span class="text-12px">头</span>
                  </p>
                  <span>平均捕虫量</span>
                  <span>第一代</span>
                </div>
                <n-divider vertical class="self-center !h-30px !-mt-10px" />
                <div class="flex-y-center flex-col">
                  <p class="mb-5px text-16px">
                    7
                    <span class="text-12px">%</span>
                  </p>
                  <span>发生率</span>
                  <span>第一代</span>
                </div>
              </div>
            </n-card>
          </div>
        </div>
        <div class="chart3">
          <div class="h-full flex-vertical">
            <div class="flex-y-center gap-5px">
              <icon-local-prevention class="text-icon text-primary" />
              <span class="text-16px text-primary font-bold">发生与防治</span>
            </div>
            <div ref="chart3Ref" class="h-full"></div>
            <n-card
              :bordered="false"
              size="small"
              class="border-l-6 rounded-0 bg-transparent bg-gradient-to-r"
              :style="{
                backgroundImage: `linear-gradient(to right, ${mixColor(
                  theme.themeColor,
                  colors2[0],
                  0.7
                )}40 , transparent)`,
                borderLeftColor: mixColor(theme.themeColor, colors2[0], 0.7)
              }"
            >
              <template #header>
                <div :style="{ color: mixColor(theme.themeColor, colors2[0], 0.7) }">常年平均情况</div>
              </template>
              <div class="flex-x-center gap-25px">
                <div class="flex-y-center flex-col">
                  <p class="mb-5px text-16px">
                    62.9
                    <span class="text-12px">天</span>
                  </p>
                  <span>发生天数</span>
                  <span>第一代</span>
                </div>
                <n-divider vertical class="self-center !h-30px !-mt-10px" />
                <div class="flex-y-center flex-col">
                  <p class="mb-5px text-16px">
                    180.4
                    <span class="text-12px">头</span>
                  </p>
                  <span>平均捕虫量</span>
                  <span>第一代</span>
                </div>
                <n-divider vertical class="self-center !h-30px !-mt-10px" />
                <div class="flex-y-center flex-col">
                  <p class="mb-5px text-16px">
                    7
                    <span class="text-12px">%</span>
                  </p>
                  <span>发生率</span>
                  <span>第一代</span>
                </div>
              </div>
            </n-card>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { useThemeStore } from '@/store';
import { useEcharts } from '@/hooks';
import { mixColor } from '@/utils';
import type { TimeOption } from '@/components/business/TimeLine.vue';
import data from './data/life-expectancy-table.json';

const theme = useThemeStore();

const timeOptions: TimeOption[] = [];
const timeRange = [2013, 2023];
// 根据timeRange获取其中所有的年份选项
for (let i = timeRange[0]; i <= timeRange[1]; i += 1) {
  timeOptions.unshift({
    label: i,
    value: i
  });
}
const year = ref(2023);

// const colors = ['bg-#3cc43c', 'bg-#368c43', 'bg-#135ef3', 'bg-#1120ef', 'bg-#dc4b38'];
const colors = ['#3cc43c', '#368c43', '#135ef3', '#1120ef', '#dc4b38'];
// const colors2 = [
//   'from-#4472ee/25 border-l-#4472ee',
//   'from-#508666/25 border-l-#508666',
//   'from-#c06874/25 border-l-#c06874'
// ];
const colors2 = ['#4472ee', '#508666', '#c06874'];
const colors3 = computed(() => {
  return ['#4472ee', '#508666', '#c06874'].map(color => {
    return mixColor(theme.themeColor, color, 0.7);
  });
});

const tabOptions = [
  {
    label: '二化螟',
    value: '1'
  },
  {
    label: '性诱',
    value: '2'
  },
  {
    label: '灯诱',
    value: '3'
  },
  {
    label: '卵',
    value: '4'
  },
  {
    label: '卷叶率',
    value: '5'
  },
  {
    label: '玉米螟',
    value: '6'
  }
];
const statisticalItems = [
  {
    type: '调查区县',
    num: 56,
    unit: '个',
    county: '万年县',
    dataTime: '05-23'
  },
  {
    type: '发生区县',
    num: 51,
    unit: '个',
    county: '通河县',
    dataTime: '05-13'
  },
  {
    type: '调查网点',
    num: 313,
    unit: '个',
    county: '甘南县',
    dataTime: '05-21'
  },
  {
    type: '发生网点',
    num: 205,
    unit: '个',
    year: 2023,
    county: '万年县',
    dataTime: '05-21'
  },
  {
    type: '发生网点',
    num: 205,
    unit: '个',
    year: 2023,
    county: '万年县',
    dataTime: '05-21'
  }
];

const { domRef: chart1Ref, updateOptions: updateOptions1 } = useEcharts(() => ({
  grid3D: {},
  tooltip: {},
  xAxis3D: {
    type: 'category'
  },
  yAxis3D: {
    type: 'category'
  },
  zAxis3D: {},
  visualMap: {
    max: 1e8,
    dimension: 'Population'
  },
  dataset: {
    dimensions: ['Income', 'Life Expectancy', 'Population', 'Country', { name: 'Year', type: 'ordinal' }],
    source: []
  },
  series: [
    {
      type: 'bar3D',
      // symbolSize: symbolSize,
      shading: 'lambert',
      encode: {
        x: 'Year',
        y: 'Country',
        z: 'Life Expectancy',
        tooltip: [0, 1, 2, 3, 4]
      }
    }
  ]
}));
async function mockData1() {
  await new Promise(resolve => {
    setTimeout(resolve, 1000);
  });

  updateOptions1(opts => {
    opts.dataset.source = data;

    return opts;
  });
}

const { domRef: chart2Ref, updateOptions: updateOptions2 } = useEcharts(
  () => ({
    color: colors3.value,
    tooltip: {
      trigger: 'axis',
      axisPointer: {
        type: 'cross'
      }
    },
    grid: {
      left: '20%',
      bottom: '10%'
    },
    toolbox: {
      feature: {
        dataView: { show: true, readOnly: false },
        saveAsImage: { show: true }
      }
    },
    legend: {
      data: ['Evaporation', 'Precipitation', 'Temperature']
    },
    xAxis: [
      {
        type: 'category',
        axisTick: {
          alignWithLabel: true
        },
        // prettier-ignore
        data: ['Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun', 'Jul', 'Aug', 'Sep', 'Oct', 'Nov', 'Dec']
      }
    ],
    yAxis: [
      {
        type: 'value',
        name: 'Evaporation',
        position: 'left',
        alignTicks: true,
        axisLine: {
          show: true,
          lineStyle: {
            color: colors3.value[0]
          }
        },
        axisLabel: {
          formatter: '{value} ml'
        }
      },
      {
        type: 'value',
        name: 'Precipitation',
        position: 'left',
        alignTicks: true,
        offset: 60,
        axisLine: {
          show: true,
          lineStyle: {
            color: colors3.value[1]
          }
        },
        axisLabel: {
          formatter: '{value} ml'
        }
      },
      {
        type: 'value',
        name: '温度',
        position: 'right',
        alignTicks: true,
        axisLine: {
          show: true,
          lineStyle: {
            color: colors3.value[2]
          }
        },
        axisLabel: {
          formatter: '{value} °C'
        }
      }
    ],
    series: [
      {
        name: 'Evaporation',
        type: 'bar',
        data: [2.0, 4.9, 7.0, 23.2, 25.6, 76.7, 135.6, 162.2, 32.6, 20.0, 6.4, 3.3]
      },
      {
        name: 'Precipitation',
        type: 'bar',
        yAxisIndex: 1,
        data: [2.6, 5.9, 9.0, 26.4, 28.7, 70.7, 175.6, 182.2, 48.7, 18.8, 6.0, 2.3]
      },
      {
        name: 'Temperature',
        type: 'line',
        yAxisIndex: 2,
        data: [2.0, 2.2, 3.3, 4.5, 6.3, 10.2, 20.3, 23.4, 23.0, 16.5, 12.0, 6.2]
      }
    ]
  }),
  {
    onRender: () => {}
  }
);
async function mockData2() {
  await new Promise(resolve => {
    setTimeout(resolve, 1000);
  });

  updateOptions2(opts => {
    opts.xAxis.data = ['06:00', '08:00', '10:00', '12:00', '14:00', '16:00', '18:00', '20:00', '22:00', '24:00'];
    opts.series[0].data = [4623, 6145, 6268, 6411, 1890, 4251, 2978, 3880, 3606, 4311];
    opts.series[1].data = [2208, 2016, 2916, 4512, 8281, 2008, 1963, 2367, 2956, 678];

    return opts;
  });
}

const { domRef: chart3Ref, updateOptions: updateOptions3 } = useEcharts(() => ({
  tooltip: {
    trigger: 'axis',
    axisPointer: {
      type: 'cross',
      label: {
        backgroundColor: '#6a7985'
      }
    }
  },
  legend: {},
  grid: {
    left: '3%',
    right: '4%',
    bottom: '3%',
    containLabel: true
  },
  xAxis: {
    type: 'category',
    boundaryGap: false,
    data: [] as string[]
  },
  yAxis: {
    type: 'value'
  },
  series: [
    {
      color: '#8e9dff',
      name: '防治量',
      type: 'line',
      smooth: true,
      stack: 'Total',
      areaStyle: {
        color: {
          type: 'linear',
          x: 0,
          y: 0,
          x2: 0,
          y2: 1,
          colorStops: [
            {
              offset: 0.25,
              color: '#8e9dff'
            },
            {
              offset: 1,
              color: '#fff'
            }
          ]
        }
      },
      emphasis: {
        focus: 'series'
      },
      data: [] as number[]
    },
    {
      color: '#26deca',
      name: '发生量',
      type: 'line',
      smooth: true,
      stack: 'Total',
      areaStyle: {
        color: {
          type: 'linear',
          x: 0,
          y: 0,
          x2: 0,
          y2: 1,
          colorStops: [
            {
              offset: 0.25,
              color: '#26deca'
            },
            {
              offset: 1,
              color: '#fff'
            }
          ]
        }
      },
      emphasis: {
        focus: 'series'
      },
      data: []
    }
  ]
}));
async function mockData3() {
  await new Promise(resolve => {
    setTimeout(resolve, 1000);
  });

  updateOptions3(opts => {
    opts.xAxis.data = ['06:00', '08:00', '10:00', '12:00', '14:00', '16:00', '18:00', '20:00', '22:00', '24:00'];
    opts.series[0].data = [4623, 6145, 6268, 6411, 1890, 4251, 2978, 3880, 3606, 4311];
    opts.series[1].data = [2208, 2016, 2916, 4512, 8281, 2008, 1963, 2367, 2956, 678];

    return opts;
  });
}

async function init() {
  mockData1();
  // mockData2();
  mockData3();
}
init();
</script>

<style scoped lang="scss">
.wrapper {
  overflow: hidden;
  display: grid;
  grid-gap: 10px;
  grid-template-columns: 150px 2fr 1fr;
  grid-template-rows: 1fr 3fr 7fr 15fr;
  grid-template-areas:
    'title select  right'
    'year statistics1 right'
    'year statistics2 right'
    'year chart1 right';

  .title {
    grid-area: title;
  }
  .year {
    grid-area: year;
  }
  .select {
    grid-area: select;
  }
  .statistics1 {
    grid-area: statistics1;
  }
  .statistics2 {
    grid-area: statistics2;
  }
  .chart1 {
    overflow: hidden;
    grid-area: chart1;
  }
  .right {
    grid-area: right;
  }
}
.right {
  overflow: hidden;
  display: grid;
  grid-gap: 20px;
  grid-template-rows: 1fr 1fr;
  grid-template-areas:
    'chart2'
    'chart3';

  .chart2 {
    overflow: hidden;
    grid-area: chart2;
  }
  .chart3 {
    overflow: hidden;
    grid-area: chart3;
  }
}
</style>
