<script setup>
import { useMainStore } from '@/stores/index.js'
const mainStore = useMainStore()

const props = defineProps({
  content: Object,
})


const submitButton = () => {
  mainStore.modal = false
  mainStore.currentAnswer = []
  if (mainStore.currentStep < mainStore.endStep) {
    mainStore.currentStep = mainStore.currentStep + 1 
  } else {
    mainStore.pollStatus = false
  }
}

</script>

<template lang="pug">
.modal
  .modal__dialog
    .modal__button-close(
      @click='mainStore.modal=false'
    )

    .modal__heading(
      v-if="props.content && props.content.title"
    ) {{ props.content.title }}
    .modal__body(
      v-if="props.content && props.content.text"
      v-html="props.content.text"
    )
    .modal__footer
      .button(
        @click="submitButton"
      ) Продолжить
</template>

<style lang="scss" scoped>
.modal {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100vh;
  background-color: rgba(0,0,0, .7);
  z-index: 100;
  display: flex;
  justify-content: center;
  align-items: center;
  &__button-close {
    position: absolute;
    width: 15px;
    height: 15px;
    right: 30px;
    top: 30px;
    cursor: pointer;
    &::after {
      content: '';
      position: absolute;
      height: 2px;
      width: 15px;
      background-color: #000;
      border-radius: 6px;
      transform: rotate(45deg)
    }
    &::before {
      content: '';
      position: absolute;
      height: 2px;
      width: 15px;
      background-color: #000;
      border-radius: 6px;
      transform: rotate(135deg)
    }
  }
  &__dialog {
    position: relative;
    width: 725px;
    background-color: #fff;
    height: 90vh;
    box-shadow: 0px 2px 4px 0px rgba(0, 0, 0, 0.10), 0px 1px 10px 0px rgba(0, 0, 0, 0.05);
    border-radius: 12px;
    overflow: hidden;
  }
  &__heading {
    height: 105px;
    font-size: 24px;
    font-style: normal;
    font-weight: 700;
    line-height: 32px;
    padding: 50px;
  }
  &__body {
    font-size: 18px;
    font-style: normal;
    font-weight: 400;
    line-height: 24px;
    padding: 0 33px;
    margin: 0 10px 30px 17px;
    height: calc(100% - 235px);
    overflow: auto;
    ::v-deep {
      font-family: 'Inter', sans-serif;
      a {
        font-weight: 500;
      }
      ul {
        list-style: none;
        padding: 0;
        margin: 0;
        li {
          position: relative;
          padding-left: 23px;
          margin-bottom: 15px;
          &::after {
            content: '';
            width: 11px;
            height: 11px;
            background-color: #6941C6;
            border-radius: 50%;
            position: absolute;
            left: 0;
            top: 6px;

          }
        }
        &.list-check {
          li {
            padding-left: 31px;
            &::before {
              content: '';
              border-radius: 25px;
              background: #D3BBFF;
              width: 22px;
              height: 22px;
              position: absolute;
              top: 0;
              left: 0;
            }
            &::after {
              border-radius: 25px;
              background: transparent url('/images/list-check.svg') 0 0 no-repeat;
              width: 22px;
              height: 22px;
              position: absolute;
              top: -5px;
              left: 6px;
            }
          }
        }
      }
      
      h3 {
      color: rgba(66, 40, 201, 0.50);
      font-family: Inter;
      font-size: 18px;
      font-style: normal;
      font-weight: 400;
      line-height: 20px;
      strong {
        color: #6941C6;
        font-size: 20px;
        font-style: normal;
        font-weight: 700;
        line-height: 28px;
      }
    }
    }
  }
  &__footer {
    display: flex;
    height: 100px;
    padding: 16px 40px;
    justify-content: flex-end;
    align-items: center;
    gap: 24px;
    background: var(--Secondary-Gray-1, #F7F7F9);
  }

}
</style>