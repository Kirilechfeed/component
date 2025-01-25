<script setup lang="ts">
import { onMounted, ref } from 'vue'
import CustomerReview from '@/components/CustomerReview.vue'
import type { IComment } from '@/models/models'
const data = ref<IComment[]>([])
const langs = {
  ua: {
    title: 'Відгуки наших клієнтів у Google',
    description: 'вiдкуги',
    buttonPrimary: 'Написати',
    buttonSecondary: 'Переглянути',
  },
  en: {
    title: 'Reviews from our clients on Google',
    description: 'reviews ',
    buttonPrimary: 'Write',
    buttonSecondary: 'Look',
  },
}

//решил реализловать Интернационализацию просто через обьект, но можно было и через библиотеку i18n
const choicedLang = ref({
  title: 'Відгуки наших клієнтів у Google',
  description: 'вiдкуги',
  buttonPrimary: 'Написати',
  buttonSecondary: 'Переглянути',
})
async function getRating() {
  const response = await fetch('https://679378dc5eae7e5c4d8ec5d6.mockapi.io/api/project/comments')
  data.value = await response.json()
}
onMounted(() => {
  getRating()
})

const choiceLang = (lang: string) => {
  if (lang == 'ua') {
    Object.assign(choicedLang.value, langs.ua)
  }
  if (lang == 'en') {
    Object.assign(choicedLang.value, langs.en)
  }
}
</script>

<template>
  <div class="header">
    <span class="lang" @click="choiceLang('ua')">UA</span> |
    <span class="lang" @click="choiceLang('en')">EN</span>
  </div>
  <div v-if="data.length">
    <CustomerReview :rating="data[0].rating" :reviews="data[0].reviews" :langs="choicedLang" />
  </div>
</template>

<style scoped>
header {
  line-height: 1.5;
  max-height: 100vh;
}
.header {
  padding: 40px 10px;
  color: rgb(118, 118, 118);
  font-size: 20px;
  display: flex;
  align-items: center;
  justify-content: end;
  gap: 5px;
}
.lang {
  font-weight: 700;
  cursor: pointer;
  transition: 0.3s ease-in;
}

.lang:hover {
  color: rgb(73, 73, 73);
}
</style>
