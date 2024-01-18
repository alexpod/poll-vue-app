<script setup>
import { onMounted } from 'vue'
import { RouterView } from 'vue-router'

import { useMainStore } from '@/stores/index.js'

const mainStore = useMainStore()

onMounted(() => {
  // mainStore.getModal()
  /* if (localStorage.getItem('steps')) {
    const steps = localStorage.getItem('steps')
    const status = localStorage.getItem('status')
    const result = localStorage.getItem('result')
    
    mainStore.resultAnswers = parseInt(result)    
    mainStore.currentStep = parseInt(steps) + 1

    if (status) mainStore.pollStatus = false
  } */
});
</script>

<template lang="pug">
.page
  RouterView
</template>

<style scoped>
</style>
