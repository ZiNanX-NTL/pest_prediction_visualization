<template>
  <hover-container class="h-full w-40px" tooltip-content="全屏" :inverted="theme.header.inverted" @click="toggle">
    <icon-gridicons-fullscreen-exit v-if="isFullscreen" class="text-18px" />
    <icon-gridicons-fullscreen v-else class="text-18px" />
  </hover-container>
</template>

<script setup>
import { useFullscreen } from '@vueuse/core';
import { useThemeStore } from '@/store';
import HoverContainer from './HoverContainer.vue';

defineOptions({ name: 'FullScreen' });

const { isFullscreen, toggle } = useFullscreen();
const theme = useThemeStore();
</script>

<style scoped></style>
