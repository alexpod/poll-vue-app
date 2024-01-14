<script setup>
import { useMainStore } from '@/stores/index.js'
const mainStore = useMainStore();

</script>

<template lang="pug">
.step-finally
  .step-finally__result количество баллов: {{ mainStore.resultAnswers }}
  h1 Вы супер-HR!
  p Вы ознакомились с резюме Павла, и оно точно соответствует вашим требованиям к кандидату!
  p Получив от вас приглашение, Павел расспрашивает вас о вакансии и компании, что говорит о том, что кандидат совсем не запомнил ваше предложение. Он не проявляет мотивации на прохождение собеседования и, к сожалению, берет время на «подумать». 
  p 
    strong Чтобы помочь избежать подобной ситуации с вашей реальной вакансией, мы подготовили руководство по работе. Заполните форму и получите наши рекомендации:
  form(
    @click.prevent=""
  )
    input(type="text" placeholder="Ваше имя")
    input(type="email" placeholder="Электронная почта (рабочая)")
    button.button(
      type="submit"
    ) Скачать <img src="/images/download.svg" alt="download" />
</template>

<style lang="scss" scoped>
.step-finally {
  padding-top: 134px;
  h1 {
    color: #D90324;
    font-family: Inter;
    font-size: 48px;
    font-style: normal;
    font-weight: 700;
    line-height: 60px; 
    margin-top: 0;
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
  }
}
form {
  display: flex;
  align-items: center;
  gap: 20px;
  flex-direction: column;
  align-items: flex-start;
  width: 432px;
  
  input {
    width: 100%;
  }
  button {
    width: 100%;
    display: flex;
  }
}
</style>