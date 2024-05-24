<template>
  <div
    class="big-layout relative size-full overflow-hidden bg-([length:100%_100%] [url(@/assets/images/big_bg.jpeg)] #05101f center no-repeat)"
  >
    <HeadBar class="h-$header-height" />
    <global-content
      class="size-full flex-vertical-full before-(block h-$header-height content-[''])"
      :show-padding="false"
    />
  </div>
  <setting-drawer />
</template>

<script setup>
import { useThemeStore } from '@/store';
import { GlobalContent } from '../common';
import { HeadBar, SettingDrawer } from './components';

defineOptions({ name: 'BigLayout' });

const theme = useThemeStore();
const headerHeight = computed(() => `${theme.header.height}px`);
</script>

<style scoped>
.big-layout {
  --header-height: v-bind(headerHeight);
}
</style>
