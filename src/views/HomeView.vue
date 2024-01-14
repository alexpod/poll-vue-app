<script setup>
import { onMounted } from 'vue'
import WindowPanelInfo from '@/components/WindowPanelInfo.vue'
import WindowSection from '@/components/WindowSection.vue'
import ModalDialog from '@/components/ModalDialog.vue'
import PollSteps from '@/components/PollSteps.vue'
import StepsPollTwo from '@/components/StepsPollTwo.vue'
import StepsPollThree from '@/components/StepsPollThree.vue'
import StepFinally from '@/components/StepFinally.vue'

import { useMainStore } from '@/stores/index.js'

const mainStore = useMainStore()

onMounted(() => {
  mainStore.getPolls()
  mainStore.getModal()
});
</script>

<template lang="pug">

ModalDialog(
  v-if="mainStore.modal"
  :content="mainStore.getModal()"
)

WindowSection
  WindowPanelInfo(
    v-if="mainStore.pollStatus"
  )
  PollSteps(
    v-if="mainStore.currentStep === 1"
    v-for="item in mainStore.polls"
    :content="item"
  )
  StepsPollTwo(
    v-if="mainStore.currentStep === 2"
    v-for="item in mainStore.polls"
    :content="item"
  )
  StepsPollThree(
    v-if="mainStore.currentStep === 3"
    v-for="item in mainStore.polls"
    :content="item"
  )
  StepFinally(
    v-if="!mainStore.pollStatus"
  )
  
</template>

<style lang="scss">
.steps {
  color: #6C12ED;
  display: inline-flex;
  padding: 20px;
  flex-direction: column;
  align-items: flex-start;
  gap: 10px;
  border-radius: 10px;
  background: #F7F7F9;
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
    &-bar {
      width: 33%;
      background-color: #6C12ED;
      height: 2px;
    }
  }
}
.poll {
  padding-top: 154px;
  max-width: 846px;
  &__question {
    color: #000;
    font-family: Inter;
    font-size: 36px;
    font-style: normal;
    font-weight: 700;
    line-height: 44px;
    margin-bottom: 60px;
    max-width: 846px;
  }
  &__subtitle {
    color: #616161;
    font-family: Inter;
    font-size: 20px;
    font-style: normal;
    font-weight: 400;
    line-height: 28px;
    margin-bottom: 10px;
  }
  &__answers {
    margin-bottom: 80px;
    max-width: 620px;
  }
  &__message {
    padding-top: 15px;
    &-title {
      font-size: 20px;
      font-style: normal;
      font-weight: 700;
      line-height: 28px;
      margin-bottom: 5px;
    }
    &-description {
      font-size: 14px;
      font-style: normal;
      font-weight: 400;
      line-height: 21px;
      color: rgba(35, 35, 37, 0.80);
    }
  }
  &__option {
    border-radius: 10px;
    border: 1px solid #E0E2E7;
    background: #F7F7F9;
    padding: 20px;
    font-size: 20px;
    margin-bottom: 10px;
    padding-left: 60px;
    cursor: pointer;
    position: relative;
    &::before {
      content: '';
      position: absolute;
      left: 20px;
      top: 20px;
      display: block;
      width: 24px;
      height: 24px;
      border: 1px solid #E0E2E7;
      border-radius: 50%;
    }
    &:hover {
      &::before {
        border-color: #6C12ED;
      }  
    }
    &.wrong {
      background-color: #FFDBDB;
    }
    &.disabled {
      cursor: default;
      &:hover {
        &::before {
          border-color: #E8F3C9;
        }  
      }
    }
    &.active {
      &::before {
        border-color: #6C12ED;
      }
      &::after {
        content: '';
        display: block;
        width: 14px;
        border-radius: 50%;
        background-color: #6C12ED;
        height: 14px;
        position: absolute;
        top: 26px;
        left: 26px;
      }
      
      &.correct {
        color: #249F5D;
        font-size: 18px;
        line-height: 24px;
        background: #E8F3C9;
        &::before {
          border-color: #249F5D;
          background-color: #fff;
        }
        &::after {
          background-color: #249F5D;
        }
      }
      
      &.incorrect {
        color: #F32D2D;
        background: #FFDBDB;
        &::before {
          border-color: #F32D2D;
          background-color: #fff;
        }
        &::after {
          background-color: #F32D2D;
        }
        .poll__message-title {
          color: rgba(139, 0, 0, 0.80);
          font-size: 20px;
          font-style: normal;
          font-weight: 700;
          line-height: 28px;
        }
        .poll__message-description {
          color: rgba(139, 0, 0, 0.80);
          font-size: 14px;
          font-style: normal;
          font-weight: 400;
          line-height: 18px;
        }
      }
    }
  }
  &__button {
    margin-top: 78px;
  }
}
</style>