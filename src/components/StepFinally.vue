<script setup>
import { ref } from 'vue'
import { useMainStore } from '@/stores/index.js'
const mainStore = useMainStore()

const name = defineModel('name')
const email = defineModel('title')
const formSuccess = ref(false)
const formError = ref(false)


const checkForm = () => {
  formError.value = false
  if (name.value && email.value) return formSuccess.value = true
  formError.value = true
}

const resetForm = () => {
  mainStore.currentStep = 1
  mainStore.resultAnswers = 0
  mainStore.pollStatus = true
  localStorage.clear()
}

const restartPoll = () => {
  // mainStore.getPolls()
  setTimeout(resetForm, 500)
}

</script>

<template lang="pug">
.step-finally__wrapper
  .step-finally__image
    img(
      src="/images/step-4.svg"
      alt=""
    )
  .step-finally
    .step-finally__result количество баллов: {{ mainStore.resultAnswers }}
    h1 Вы супер-HR!
    p Вы ознакомились с резюме Павла, и оно точно соответствует вашим требованиям к кандидату!
    p Получив от вас приглашение, Павел расспрашивает вас о вакансии и компании, что говорит о том, что кандидат совсем не запомнил ваше предложение. Он не проявляет мотивации на прохождение собеседования и, к сожалению, берет время на «подумать». 
    p 
      strong Чтобы помочь избежать подобной ситуации с вашей реальной вакансией, мы подготовили руководство по работе. Заполните форму и получите наши рекомендации:
    form(
      v-if="!formSuccess"
      @submit.prevent="checkForm"
    )
      input(type="text" v-model="name" placeholder="Ваше имя")
      input(type="text" v-model="email" placeholder="Электронная почта (рабочая)")
      p.message__error(
        v-if="formError"
      ) Заполните все поля
      button.button(
        type="submit"
      ) Скачать <img src="/images/download.svg" alt="download" />
    .form__success(
      v-if="formSuccess"
    )
      p.message__success <strong>Форма отправлена</strong> скоро начнется загрузка файла
      .button(
        @click="restartPoll"
      ) Пройти опрос повторно
</template>

<style lang="scss" scoped>
.step-finally {
  padding-top: 134px;
  max-width: 680px;
  @media (max-width: 1480px) {
    font-size: 14px;
    padding-top: 20px;
  }
  &__image {
    @media (min-width: 1481px) {
      position: absolute;
      bottom: auto;
      right: 0px;
      top: 0px;
    }

    padding-top: 112px;
    @media (max-width: 1480px) {
      padding: 20px 0 10px;
      
    }
    img {
      @media (max-width: 1480px) {
        max-width: 240px;
        display: block;
        margin: auto;
      }
    }
  }
  p {
    strong {
      display: block;
      padding-top: 10px;
      padding-bottom: 20px;
    }
  }
  h1 {
    color: #D90324;
    font-family: Inter;
    font-size: 48px;
    font-style: normal;
    font-weight: 700;
    line-height: 60px; 
    margin-top: 0;
    @media (max-width: 1480px) {
      font-size: 30px;
      line-height: 44px;
    }
  }
  &__result {
    border-radius: 5px;
    border: 1px solid var(--Gray-2, #E0E2E7);
    color: rgba(0, 0, 0, 0.60);
    font-family: Inter;
    font-size: 14px;
    font-style: normal;
    font-weight: 700;
    line-height: 24px;
    letter-spacing: 1.4px;
    text-transform: uppercase;
    margin-bottom: 30px;
    display: inline-flex;
    padding: 10px 15px;
    align-items: flex-start;
    gap: 10px;
    @media (max-width: 1480px) {
      margin-bottom: 15px;
    }
  }
}
form {
  display: flex;
  align-items: center;
  gap: 20px;
  flex-direction: column;
  align-items: flex-start;
  width: 432px;
  @media (max-width: 1480px) {
    width: auto;
    font-size: 14px;
  }
  
  input {
    width: 100%;
    @media (max-width: 1480px) {
     
      font-size: 14px;
    }
  }
  button {
    width: 100%;
    display: flex;
  }
}
.message {
  &__success {
    color: #249F5D;
    font-size: 18px;
    line-height: 24px;
    background: #E8F3C9;
    padding: 20px;
    border-radius: 8px;
  }
  &__error {
    width: 100%;
    font-size: 18px;
    line-height: 24px;
    color: #F32D2D;
    background: #FFDBDB;
    padding: 20px;
    border-radius: 8px;
  }
}
</style>