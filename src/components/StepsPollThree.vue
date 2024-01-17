<script setup>
import { onMounted, ref, reactive } from 'vue'
import { useMainStore } from '@/stores/index.js'
const mainStore = useMainStore();

const props = defineProps({
  content: Object
})

let message = reactive([])
const answerValidated = ref(false)
let itemsRef = [];

const optionChosen = (element) => {
  if (element) {
    itemsRef.push(element);
  }
};

const selectOption = (item) => {
  if (!answerValidated.value) {
    item.active = !item.active
    if (item.active) mainStore.currentAnswer = [...mainStore.currentAnswer, item]
    else mainStore.currentAnswer= mainStore.currentAnswer.filter(arr => arr.id !== item.id)
  }
}

const submitButton = () => {
  if (answerValidated.value) return mainStore.modal = true
  validateForm()
}

const validateForm = () => {
  if (mainStore.currentAnswer.length !== 0) {
    
    props.content.options.map(item => {
      if (props.content.answer.includes(item.id)) {
        item.status = 'disabled correct'
      }  else {
        item.status = 'disabled incorrect'
      }
    })
    
    answerValidated.value = true
    let countNumber = mainStore.currentAnswer.filter((item) => item.status === 'disabled correct').length
    if (countNumber === 3) {
      mainStore.resultAnswers += 1
      localStorage.setItem('result', mainStore.resultAnswers)
      localStorage.setItem('steps', mainStore.currentStep)
      localStorage.setItem('status', 1)
      return message = {
        title: 'Бинго!',
        description: `Аналитика по этап подбора – это сервис, позволяющий узнать эффективность 
          вашей воронки найма в разрезе показателей каждого ее этапа – от количества просмотров 
          до количества нанятых кандидатов <strong>читать еще</strong>`,
        status: 'correct'
      }
    } else if (countNumber > 0) {
      localStorage.setItem('steps', mainStore.currentStep)
      localStorage.setItem('status', 1)
      return message = {
        title: 'Не совсем верно...',
        description: `Аналитика по этап подбора – это сервис, позволяющий узнать эффективность 
          вашей воронки найма в разрезе показателей каждого ее этапа – от количества просмотров 
          до количества нанятых кандидатов <strong>читать еще</strong>`,
        status: 'incorrect'
      }
    } else {
      localStorage.setItem('steps', mainStore.currentStep)
      localStorage.setItem('status', 1)
      return message = {
        title: 'К сожалению, неверно',
        description: `Аналитика по этап подбора – это сервис, позволяющий узнать эффективность 
          вашей воронки найма в разрезе показателей каждого ее этапа – от количества просмотров 
          до количества нанятых кандидатов <strong>читать еще</strong>`,
        status: 'incorrect'
      }
    }
  }
}

onMounted(() => {
  optionChosen
});
</script>

<template lang="pug">
.poll__wrapper
  .poll__image
    img(
      src="/images/step-3.svg"
      alt=""
    )
  .poll(
    v-if="props.content.id === 3 && mainStore.pollStatus"
  )
    .poll__subtitle(
      v-if="props.content.subtitle"
    ) {{ props.content.subtitle }}
    .poll__question {{ props.content.question }}
    .poll__answers
      .poll__option(
        v-for="(item, index) in props.content.options"
        :key="item.id"
        :class="[{'active': item.active}, item.status]"
        @click="selectOption(item, index)"
      )
        span {{ item.value }}
        .poll__message(
          v-if="message.title && item.id === mainStore.currentAnswer.id"
        )
      .poll__message(
        v-if="message && message.title"
        :class="message.status"
      )
        .poll__message-title {{ message.title }}
        .poll__message-description(
          v-html="message.description"
        )
      .button.poll__button(
        :class="{'disabled': mainStore.currentAnswer.length === 0}"
        @click="submitButton"
      ) Продолжить
</template>

<style lang="scss" scoped>
.poll {
  &__image {
    @media (min-width: 1481px) {
      position: absolute;
      right: 40px;
      top: 300px;
    }
    img {
      @media (max-width: 1480px) {
        max-width: 272px;
      }
    }
  }
  &__message {
    padding: 20px;
    &-description {
      font-size: 14px;
      font-style: normal;
      font-weight: 600;
      line-height: 21px;
    }
    &.correct {
      border-radius: 8px;
      background: #E8F3C9;
      .poll__message-title {
        color: #249F5D;
        margin-bottom: 5px;
      }
    }
    &.incorrect {
      border-radius: 8px;
      background: #FFDBDB;
      .poll__message-title {
        color: #F32D2D;
        margin-bottom: 5px;
      }
    }
  }
  &__option {
    &::before {
      border-radius: 5px;
    }
    &.active {
      &::before {
        background-color: #6C12ED;
      }
      &::after {
        background: transparent url('/images/icon-check.svg') center center no-repeat;
      }
      &.correct {
        font-size: 14px;
        &::before {
          background-color: #37B94A;
        }
        &::after {
          background-color: transparent;
        }
      }
      &.incorrect {
        font-size: 14px;
        &::before {
          background-color: #F32D2D;
        }
        &::after {
          background-color: transparent;
        }
      }
    }
  }
}
</style>