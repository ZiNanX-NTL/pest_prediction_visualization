<template>
  <n-drawer :show="app.settingDrawerVisible" display-directive="show" :width="330" @mask-click="app.closeSettingDrawer">
    <n-drawer-content title="主题配置" :native-scrollbar="false">
      <theme-color-select />
      <n-divider title-placement="center">界面功能</n-divider>
      <n-space vertical size="large">
        <setting-menu label="头部高度">
          <n-input-number
            class="w-120px"
            size="small"
            :value="theme.header.height"
            :step="1"
            @update:value="theme.setHeaderHeight"
          />
        </setting-menu>
      </n-space>
    </n-drawer-content>
  </n-drawer>
</template>

<script setup lang="ts">
import { useAppStore, useThemeStore } from '@/store';
import { ThemeColorSelect, SettingMenu } from '../../common/setting-drawer/components';

defineOptions({ name: 'SettingDrawer' });

const app = useAppStore();
const theme = useThemeStore();
</script>

<style scoped></style>
