<template>
  <div v-if="showTooltip">
    <n-tooltip :placement="placement" trigger="hover">
      <template #trigger>
        <div class="h-full flex-center cursor-pointer dark:hover:bg-#33333350" :class="contentClassName">
          <slot></slot>
        </div>
      </template>
      {{ tooltipContent }}
    </n-tooltip>
  </div>
  <div v-else class="flex-center cursor-pointer dark:hover:bg-#33333350" :class="contentClassName">
    <slot></slot>
  </div>
</template>

<script setup>
defineOptions({ name: 'HoverContainer' });

const props = defineProps({
  /** tooltip显示文本 */
  tooltipContent: {
    type: String,
    default: ''
  },
  /** tooltip的位置 */
  placement: {
    type: String,
    default: 'bottom'
  },
  /** class类 */
  contentClass: {
    type: String,
    default: ''
  },
  /** 反转模式下 */
  inverted: {
    type: Boolean,
    default: false
  }
});

const showTooltip = computed(() => Boolean(props.tooltipContent));

const contentClassName = computed(
  () => `${props.contentClass} ${props.inverted ? 'hover:bg-primary' : 'hover:bg-#f6f6f6'}`
);
</script>

<style scoped></style>
