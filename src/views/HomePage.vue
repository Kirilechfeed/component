<script setup lang="ts">
import { onMounted, ref } from 'vue'
import CustomerReview from '@/components/CustomerReview.vue'
import type { IComment } from '@/module/module'
const data = ref<IComment[]>([])

async function getRating() {
  const response = await fetch('https://679378dc5eae7e5c4d8ec5d6.mockapi.io/api/project/comments')
  data.value = await response.json()
}
onMounted(() => {
  getRating()
})
</script>

<template>
  <div v-if="data.length">
    <CustomerReview :rating="data[0].rating" :reviews="data[0].reviews" />
  </div>

  <RouterView />
</template>

<style scoped>
header {
  line-height: 1.5;
  max-height: 100vh;
}
</style>
