<template>
  <div class="h-full flex justify-end">
    <full-screen />
    <setting-button v-if="showButton" />
    <user-avatar />
  </div>
</template>

<script setup lang="ts">
import { FullScreen, UserAvatar, SettingButton } from './components';

const showButton = import.meta.env.DEV;
</script>

<style lang="scss" scoped></style>
