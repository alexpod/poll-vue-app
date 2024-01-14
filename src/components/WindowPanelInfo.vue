<script setup>
import { useMainStore } from '@/stores/index.js'
const mainStore = useMainStore()
</script>

<template lang="pug">
.panel-info
  .panel-info__age 0+
  .steps
    .steps__value шаг {{ mainStore.currentStep }} / {{ mainStore.endStep }}
    .steps__progress
      .steps__progress-bar(
        :style="{ width: `${mainStore.getProgressBarWidth()}%`}"
      )
</template>

<style lang="scss" scoped>

.panel-info {
  display: flex;
  gap: 20px;
  position: absolute;
  right: 20px;
  top: 58px;
  &__age {
    color: #9CA1AD;
    font-size: 14px;
    font-weight: 500;
    display: flex;
    width: 40px;
    height: 40px;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    border-radius: 100px;
    border: 1px solid #E0E2E7;
  }
}
</style>