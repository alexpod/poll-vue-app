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
  top: 20px;
  @media (max-width: 1480px) {
    flex-direction: row-reverse;
    position: relative;
    top: 0;
    right: 0;
    width: 100%;
    gap: 0;
  }
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
.steps {
  color: #6C12ED;
  display: inline-flex;
  padding: 20px;
  flex-direction: column;
  align-items: flex-start;
  gap: 10px;
  border-radius: 10px;
  background: #F7F7F9;
  @media (max-width: 1480px) {
    background: none;
    padding: 8px 0 0;
    margin-right: auto;
    margin-left: auto;
    padding-left: 40px;
  }
  &__value {
    font-size: 14px;
    font-style: normal;
    font-weight: 600;
    line-height: 24px;
  }
  &__progress {
    border-radius: 10px;
    overflow: hidden;
    height: 2px;
    background-color: #E0E2E7;
    width: 100%;
    @media (max-width: 1480px) {
      display: none;
    }
    &-bar {
      width: 33%;
      background-color: #6C12ED;
      height: 2px;
    }
  }
}
</style>