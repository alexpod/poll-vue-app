<script setup>
import { onMounted, watch } from 'vue'
import WindowPanelInfo from '@/components/WindowPanelInfo.vue'
import WindowSection from '@/components/WindowSection.vue'
import ModalDialog from '@/components/ModalDialog.vue'
import StepPollOne from '@/components/StepPollOne.vue'
import StepsPollTwo from '@/components/StepsPollTwo.vue'
import StepsPollThree from '@/components/StepsPollThree.vue'
import StepFinally from '@/components/StepFinally.vue'

import { useMainStore } from '@/stores/index.js'

const mainStore = useMainStore()

onMounted(() => {
  // mainStore.getPolls()
  // mainStore.getPolls()
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

  StepPollOne(
    v-if="mainStore.currentStep === 1"
    :content="mainStore.getStepContent()"
  )
  StepsPollTwo(
    v-if="mainStore.currentStep === 2"
    :content="mainStore.getStepContent()"
  )
  StepsPollThree(
    v-if="mainStore.currentStep === 3"
    :content="mainStore.getStepContent()"
  )
  StepFinally(
    v-if="!mainStore.pollStatus"
  )

.background-element
  img(src="/images/bg-element-1.svg" alt="")
  img(src="/images/bg-element-2.svg" alt="")
  img(src="/images/bg-element-3.svg" alt="")
  img(src="/images/bg-element-4.svg" alt="")
  img(src="/images/bg-element-5.svg" alt="")
</template>

<style lang="scss">
.poll {
  padding-top: 154px;
  max-width: 846px;
  @media (max-width: 1480px) {
    padding-top: 20px;
  }
  &__wrapper {
    @media (min-width: 1481px) {
      //display: flex;
      // flex-direction: row-reverse;
    }
  }
  &__image {
    @media (min-width: 1481px) {
      position: absolute;
      /* bottom: -300px;
      right: -100px; */
    }

    padding-top: 112px;
    @media (max-width: 1480px) {
      padding: 20px 0 10px;
      
    }
    img {
      @media (max-width: 1480px) {
        max-width: 70%;
        display: block;
        margin: auto;
      }
    }
  }
  &__question {
    color: #000;
    font-family: Inter;
    font-size: 36px;
    font-style: normal;
    font-weight: 700;
    line-height: 44px;
    margin-bottom: 60px;
    max-width: 846px;
    
    @media (max-width: 1480px) {
      font-size: 18px;
      font-style: normal;
      font-weight: 600;
      line-height: 24px; 
      margin-bottom: 30px;
    }
  }
  &__subtitle {
    color: #616161;
    font-family: Inter;
    font-size: 20px;
    font-style: normal;
    font-weight: 400;
    line-height: 28px;
    margin-bottom: 10px;
    @media (max-width: 1480px) {
      font-size: 14px;
      font-style: normal;
      font-weight: 400;
      line-height: 18px;
      margin-bottom: 30px;
    }
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
    @media (max-width: 1480px) {
      padding: 10px 10px 10px 45px;
      font-size: 14px;
      line-height: 18px;
    }
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
      @media (max-width: 1480px) {
        left: 9px;
        top: 9px;
        width: 19px;
        height: 19px;
      }
    }
    &:hover {
      &::before {
        border-color: #6C12ED;
        border-width: 2px;
      }  
    }
    &.wrong {
      background-color: #FFDBDB;
    }
    &.disabled {
      cursor: default;
      &:hover {
        &::before {
          border: 1px solid #E0E2E7;
        }  
      }
    }
    &.active {
      &::before {
        border-color: #6C12ED;
        border-width: 2px;
      }
      &::after {
        content: '';
        display: block;
        width: 16px;
        border-radius: 50%;
        background-color: #6C12ED;
        height: 16px;
        position: absolute;
        top: 26px;
        left: 26px;
        @media (max-width: 1480px) {
          left: 14px;
          top: 14px;
          width: 13px;
          height: 13px;
          
        }
      }
      
      &.correct {
        color: #249F5D;
        font-size: 18px;
        line-height: 24px;
        background: #E8F3C9;
        &::before {
          border-color: #249F5D;
          background-color: #fff;
          border-width: 2px;
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
          border-width: 2px;
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
          @media (max-width: 1480px) {
            font-size: 18px;
            line-height: 24px;
          }
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
    @media (max-width: 1480px) {
      margin-top: 66px;
      font-size: 18px;
    }
  }
}
.background-element {
  position: absolute;
  top: 50%;
  left: 50%;
  width: 1px;
  height: 1px;
  @media (max-width: 1480px) {
    display: none;
  }
  img:nth-child(1){
    position: absolute;
    left: -784px;
    top: -328px;
  }
  img:nth-child(2){
    position: absolute;
    left: -826px;
    top: 36px;
  }
  img:nth-child(3){
    position: absolute;
    right: -934px;
    top: -206px;
  }
  img:nth-child(4){
    position: absolute;
    top: 359px;
    right: -809px;
  }
  img:nth-child(5){
    position: absolute;
    top: 369px;
    right: -859px;
  }
}
</style>