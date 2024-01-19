<script setup>
import { onMounted, ref, reactive } from 'vue'
import { useMainStore } from '@/stores/index.js'
const mainStore = useMainStore()

const props = defineProps({
  content: {
    required: true,
    default: () => {},
  }
})

let draggableItem = ref(null)
const dropItems = ref()
let message = reactive({})



const answerValidated = ref(false)
let itemsRef = []
const optionChosen = (element) => {
  if (element) {
    itemsRef.push(element)
  }
}

const selectOption = (item, index) => {
  if (!answerValidated.value) {
    props.content.options.map(item => item.active = false)
    item.active = !item.active
    mainStore.currentAnswer = item
  }
}

const startDrag = (index) => {
  if(!answerValidated.value) draggableItem.value = index
}

const onDrop = (index) => {
  if(!answerValidated.value) {
    const dropItemsAr = props.content.options
    const itemId = dropItemsAr.splice(draggableItem.value, 1)[0]
    dropItemsAr.splice(index, 0, itemId)
    draggableItem.value = null
  }
}

const getOptionId = () => {
  const dropItemsAr = props.content.options
  return dropItemsAr.map(item => item.id)
}

const submitButton = () => {
  if (answerValidated.value) return mainStore.modal = true
  validateForm()
}

const validateForm = () => {

  props.content.options.map((item, index) => {
    if(item.id === mainStore.currentAnswer[index]) {
      item.status = 'disabled correct'
      
    } else {
      item.status = 'disabled incorrect'
    }
  })

  answerValidated.value = true

  if(getOptionId().toString() === mainStore.currentAnswer.toString()) {
    mainStore.resultAnswers += 1
    localStorage.setItem('steps', mainStore.currentStep)
    localStorage.setItem('result', mainStore.resultAnswers)
    message =  {
      title: "Абсолютно",
      description: `Мы провели опрос среди соискателей на тему того, что им интересно 
        узнать о потенциальном работодателе. Мы советуем опираться на эти данные при 
        написании описания компании. А если вы испытываете трудности <strong>читать еще</strong>`,
      status: 'correct'
    }
  } else {
    message =  {
      title: "Неверно",
      description: `Мы провели опрос среди соискателей на тему того, что им интересно 
        узнать о потенциальном работодателе. Мы советуем опираться на эти данные при 
        написании описания компании. А если вы испытываете трудности <strong>читать еще</strong>`,
      status: 'incorrect'
    }
  }
}

onMounted(() => {
  mainStore.getPolls()
  optionChosen
  mainStore.currentAnswer = [1,2,3,4]
})
</script>

<template lang="pug">
.poll__wrapper
  .poll__image
    img(
      src="/images/step-2.svg"
      alt=""
    )
  .poll(
    v-if="props.content"
  )
    .poll__subtitle(
      v-if="props.content.subtitle"
    ) {{ props.content.subtitle }}
    .poll__question {{ props.content.question }}
    .poll__answers
      .poll__option.active(
        v-for="(item, index) in props.content.options"
        :key="item.id"
        :class="[{'active': item.active}, item.status]"
        draggable="true"
        @dragstart="startDrag(index)"
        @drop="onDrop(index)"
        @dragenter.prevent
        @dragover.prevent
      )
        span.poll__index {{ index + 1}}
        span {{ item.value }}
        span.poll__arrow
      .poll__message(
        v-if="message && message.title"
        :class="message.status"
      )
        .poll__message-title {{ message.title }}
        .poll__message-description(
          v-html="message.description"
        )
      .button.poll__button(
        @click="submitButton"
      ) Продолжить
</template>

<style lang="scss" scoped>
.poll {
  &__image {
    @media (min-width: 1481px) {
      position: absolute;
      top: 200px;
      right: -100px;
    }
    img {
      @media (max-width: 1480px) {
        max-width: 172px;
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
    &:active,
    &:focus,
    &:hover {
      background-color: #7435e225;
    }
    &::before {
      display: none;
    }
    &::after {
      display: none;
    }
    &.active {
      &::after {
        display: none;
      }
      &.incorrect {
        color: #F32D2D;
        background: #FFDBDB;
        &::after {
          display: none;
        }
        .poll__index {
          background: #F32D2D;
        }
      }
      &.correct {
        color: #249F5D;
        font-size: 18px;
        line-height: 24px;
        background: #E8F3C9;
        &::after {
          display: none;
        }
        .poll__index {
          background: #249F5D;
        }
      }
    }
  }
  &__arrow {
    content: "";
    width: 28px;
    height: 28px;
    background: url('/images/icon-drop.svg') 0 0 no-repeat;
    position: absolute;
    right: 20px;
    @media (max-width: 1480px) {
      background-size: 12px;
      right: 10px;
    }
  }
  &__index {
    background-color: #7435E2;
    color: #fff;
    display: flex;
    justify-content: center;
    align-items: center;
    border-radius: 3px;
    width: 24px;
    height: 24px;
    position: absolute;
    left: 20px;
    top: 20px;
    font-size: 20px;
    font-style: normal;
    font-weight: 700;
    line-height: 28px;
    @media (max-width: 1480px) {
      top: 7px;
      left: 7px;
      font-size: 16px;
    }
    
  }
}
</style>