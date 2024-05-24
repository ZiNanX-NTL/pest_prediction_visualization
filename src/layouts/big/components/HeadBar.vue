<template>
  <div class="absolute z-10 w-full bg-([length:100%_100%] [url(@/assets/images/big_title.png)] center no-repeat)">
    <div class="size-full flex-center">
      <h1 class="translate-x-.1em text-24px tracking-0.2em -translate-y-.1em">
        <n-gradient-text
          :gradient="{
            from: theme.themeColor,
            to: '#FDFBF3'
          }"
        >
          {{ title }}
        </n-gradient-text>
      </h1>
    </div>
    <!-- 菜单 -->
    <div class="absolute-lb h-full flex items-center pb-7px">
      <template v-for="(item, index) in menuRoutes" :key="item.name">
        <n-button
          text
          tag="div"
          type="primary"
          :color="theme.themeColor"
          class="h-full px-20px text-center text-16px"
          :class="{ '!text-#ccc': route.name === item.name }"
          @click="handleToPage(item)"
        >
          {{ item.meta.title }}
        </n-button>
        <n-divider v-if="menuRoutes && index !== menuRoutes.length - 1" vertical class="!bg-#5c5c5c" />
      </template>
    </div>
    <!-- 状态 -->
    <div class="absolute-rb right-20px h-full flex items-center pb-7px">
      <HeadRight></HeadRight>
    </div>
  </div>
</template>

<script setup lang="ts">
import { routes } from '@/router';
import { useThemeStore } from '@/store';
import { getAppInfo, useRouterPush } from '@/utils';
import HeadRight from './head-right/index.vue';

defineOptions({
  name: 'HeadBar'
});

const route = useRoute();
const { routerPush } = useRouterPush();

const { title } = getAppInfo();
const theme = useThemeStore();
const menuRouteParent = routes.find((item: AuthRoute.Route) => item.name === 'pest-prediction') as
  | AuthRoute.Route
  | undefined;
const menuRoutes = ref<AuthRoute.Route[] | undefined>([]);
if (menuRouteParent) {
  menuRoutes.value = menuRouteParent.children;
}

/**
 * 路由跳转
 * @param item 自定义路由项
 */
function handleToPage(item: AuthRoute.Route) {
  const menuItem = item;
  routerPush(menuItem.path);
}
</script>

<style scoped></style>
