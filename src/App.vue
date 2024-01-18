<script setup>
import { onMounted } from 'vue'
import { RouterView } from 'vue-router'

import { useMainStore } from '@/stores/index.js'

const mainStore = useMainStore()

onMounted(() => {
})
</script>

<template lang="pug">
.page
  RouterView
</template>

<style scoped>
</style>
