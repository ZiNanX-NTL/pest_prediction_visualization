<template>
  <div ref="timelineRef" class="timeline">
    <div class="entries">
      <div v-for="item in option" :key="item.value" class="entry" :style="{ marginBottom: `${entriesMarginBottom}px` }">
        <div
          class="title cursor-pointer transition-base"
          :class="{ '!text-primary !before:border-primary big': year === item.value }"
          @click="handleSelect(item)"
        >
          {{ item.label }}
        </div>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { useElementSize } from '@vueuse/core';

/** 时间选项 */
export interface TimeOption {
  value: any;
  label: number;
}
interface Props {
  option: TimeOption[];
}
const props = defineProps<Props>();

const year = defineModel<TimeOption['value']>({ required: true });

// 获取timeline高度
const timelineRef = ref<HTMLDivElement>();
const { height: timelineHeight } = useElementSize(timelineRef);

// 获取entry的marginBottom
const entriesMarginBottom = computed(() => {
  return (timelineHeight.value - 42 * props.option.length + 40) / (props.option.length - 1);
});

/** 选择年份 */
function handleSelect(item: TimeOption) {
  year.value = item.value;
}
</script>

<style lang="scss" scoped>
$entryPadding: 20px;
$iconWidth: 8px;
$iconOffset: calc(0px - ($entryPadding + $iconWidth / 2));

.timeline {
  // background-color: #1d1d1d;
  min-height: 100%;
  margin: 0;
  font-family: 'Droid Sans', sans-serif;
  position: relative;
  padding-top: 20px;
  padding-bottom: 20px;
  border: 1px solid rgb(56, 56, 56);
  &:before {
    content: '';
    position: absolute;
    top: 20px;
    left: 50%;
    bottom: 20px;
    transform: translateX(-50%);
    width: 4px;
    background-color: #fff;
  }
  .entries {
    width: 100%;
    max-width: 800px;
    margin: auto;
    position: relative;
    .entry {
      width: 50%;
      float: left;
      padding-right: $entryPadding;
      clear: both;
      text-align: right;
      &:first-child {
        margin-top: -14px;
      }
      &:last-child {
        margin-bottom: 0px !important;
      }
      .title {
        font-size: 20px;
        margin-bottom: 12px;
        position: relative;
        color: #fff;
        &:before {
          content: '';
          position: absolute;
          width: $iconWidth;
          height: $iconWidth;
          border: 4px solid #ffffff;
          background-color: #1d1d1d;
          border-radius: 100%;
          top: 50%;
          transform: translateY(-50%);
          right: $iconOffset;
          z-index: 1000;
          transition: all 0.3s;
        }
        &.big:before {
          width: 18px;
          height: 18px;
          transform: translate(5px, -50%);
        }
      }
      .body {
        color: #aaa;
        p {
          line-height: 1.4em;
        }
      }
      &:nth-child(2n) {
        padding-left: $entryPadding;
        text-align: left;
        float: right;
        .title {
          &:before {
            left: $iconOffset;
          }
          &.big:before {
            transform: translate(-5px, -50%);
          }
        }
      }
    }
  }
}
</style>
