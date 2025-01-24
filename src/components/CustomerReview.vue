<template>
  <div class="reviews-summary">
    <div class="reviews-container">
      <div class="reviews-summary__info">
        <div class="reviews-summary__logo">
          <img src="../assets/google.svg" alt="Google" />
        </div>
        <div class="reviews-summary__text">
          <p>Відгуки наших клієнтів у Google</p>
        </div>
      </div>

      <div class="reviews-summary__rating">
        <span class="reviews-summary__rating-value">{{ rating }}</span>
        <div class="reviews-summary__stars">
          <DevSVG
            v-for="(fill, index) in fillStar"
            :key="index"
            :fill="fill"
            :id="index.toString()"
          ></DevSVG>
        </div>
        <span class="reviews-summary__count">{{ reviews }} відгуки</span>
      </div>
    </div>

    <div class="reviews-summary__actions">
      <DevButton @click="redirectToGoogle" :style="'check'">Переглянути</DevButton>
      <DevButton @click="openModal" :style="'write'">Написати</DevButton>
    </div>
  </div>
  <Transition name="modal">
    <div v-if="isModal" class="modal">Hello World</div>
  </Transition>
  <Transition name="modal">
    <div v-if="isModal" class="modal-overlay" @click="closeModal"></div>
  </Transition>
</template>

<script setup lang="ts">
import { defineProps, ref } from 'vue'
import DevButton from './/DevButton.vue'
import DevSVG from './DevSVG.vue'
const fillStar = ref<number[]>([0, 0, 0, 0, 0])
const isModal = ref(false)
interface Props {
  rating: number
  reviews: number
}
const { rating, reviews } = defineProps<Props>()

const getStarFill = () => {
  const float = Number(Number(rating % 1).toFixed(1))
  const intNumberRating = rating - Number(float)
  for (let i = 0; i < intNumberRating; i++) {
    fillStar.value[i] = 100
  }
  if (float !== 0) {
    fillStar.value[intNumberRating] = float * 100
  }
}
const redirectToGoogle = () => {
  window.location.href = 'https://www.google.com'
}
const openModal = () => {
  isModal.value = true
}
const closeModal = () => {
  isModal.value = false
}
getStarFill()
</script>

<style scoped>
.modal {
  height: 200px;
  width: 200px;
  background: #ffffff;
  box-shadow: 0px 1px 5px rgb(228, 228, 228);
  border-radius: 6px;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  opacity: 1;
  z-index: 2;
  display: flex;
  justify-content: center;
  align-items: center;
  color: black;
  font-size: 30px;
}
.modal-enter-active,
.modal-leave-active {
  transition: opacity 0.5s ease;
}

.modal-enter-from,
.modal-leave-to {
  opacity: 0;
}
.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: rgba(0, 0, 0, 0.5);
}
.reviews-summary {
  display: flex;
  align-items: center;
  box-shadow: 0px 1px 5px rgb(228, 228, 228);
  padding: 20px;
  color: #394155;
  background: #ffffff;
  max-width: 1200px;
  margin: 0 auto;
}
.reviews-container {
  display: flex;
  flex-direction: row;
  gap: 60px;
}

.reviews-summary__info {
  display: flex;
  align-items: center;
  gap: 20px;
}
.reviews-summary__text {
  font-weight: 500;
  font-size: 20px;
}
.reviews-summary__rating {
  display: flex;
  align-items: center;
  gap: 20px;
}
.reviews-summary__rating-value {
  font-size: 36px;
  line-height: 0%;
}
.reviews-summary__count {
  color: #798595;
  font-size: 14px;
}
.reviews-summary__stars {
  display: flex;
  align-items: center;
  gap: 6px;
}
.reviews-summary__actions {
  display: flex;
  align-items: center;
  flex: 1;
  justify-content: end;
  gap: 10px;
}
@media (max-width: 1199px) {
  .reviews-summary {
    display: flex;
    align-items: center;
    box-shadow: 0px 1px 5px rgb(228, 228, 228);
    padding: 20px;
    gap: 60px;
    color: #394155;
    background: #ffffff;
    max-width: 1000px;
    margin: 0 auto;
  }
  .reviews-container {
    display: flex;
    flex-direction: column;
    gap: 10px;
  }
}
@media (max-width: 720px) {
  .reviews-summary__actions {
    flex-direction: column;
  }
}
@media (max-width: 576px) {
  .reviews-summary {
    flex-direction: column;
  }
  .reviews-container {
    display: flex;
    flex-direction: column;
    gap: 10px;
  }
  .reviews-summary__actions {
    width: 100%;
  }
}
</style>
