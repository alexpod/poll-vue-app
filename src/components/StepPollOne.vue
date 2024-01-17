<script setup>
import { onMounted, ref, reactive } from 'vue'
import { useMainStore } from '@/stores/index.js'
const mainStore = useMainStore();

const props = defineProps({
  content: Object
})

let message = reactive({})

const answerValidated = ref(false)
let itemsRef = [];
const optionChosen = (element) => {
  if (element) {
    itemsRef.push(element);
  }
};

const selectOption = (item, index) => {
  if (!answerValidated.value) {
    props.content.options.map(item => item.active = false)
    item.active = !item.active
    mainStore.currentAnswer = item
  }
}

const submitButton = () => {
  if (answerValidated.value) return mainStore.modal = true
  validateForm()
}

const validateForm = () => {
  if (mainStore.currentAnswer.value) {
    props.content.options.map(item => {
      if (item.id === mainStore.currentAnswer.id && item.id === props.content.answer) {
        item.status = 'disabled correct'
        mainStore.resultAnswers = mainStore.resultAnswers + 1
        message =  {
          title: "Абсолютно верно!",
          description: `Умный поиск hh.ru устроен таким образом, чтобы кандидату 
            выдавались в первую очередь наиболее релевантные для него вакансии. 
            Алгоритм фактически понимает смысл написанного в резюме и вакансии 
            <strong>читать еще</strong>`
        }
      } else if (props.content.answer != mainStore.currentAnswer.id) {
        message =  {
          title: "Неверно",
          description: `Статистика брендированных шаблонов вакансии показывает 
            портрет кандидатов, заходящих на страницу вашей вакансии, и источники 
            Тут будет 3 строки Тут будет 3 строкиТут будет 3 строкиТут будет 3 
            строки <strong>читать еще</strong>`
        }
        item.status = 'disabled incorrect'
      } else {
        item.status = 'disabled incorrect'
      }
    })
    localStorage.setItem('steps', mainStore.currentStep);
    localStorage.setItem('result', mainStore.resultAnswers);
    answerValidated.value = true
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
      src="/images/step-1.svg"
      alt=""
    )
  .poll(
    v-if="props.content.id === mainStore.currentStep && mainStore.pollStatus"
  )
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
          .poll__message-title(
            v-if="message.title && item.id === mainStore.currentAnswer.id"
          ) {{ message.title }}
          .poll__message-description(
            v-if="message.description && item.id === mainStore.currentAnswer.id"
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
      bottom: auto;
      right: 67px;
      top: 56px;
    }
    img {
      @media (max-width: 1480px) {
        max-width: 210px;
      }
    }
  }
}
</style>