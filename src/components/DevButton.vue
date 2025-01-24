<script lang="ts" setup>
interface Props {
  style: string
}
const { style } = defineProps<Props>()

defineEmits(['click'])
</script>

<template>
  <button @click="$emit('click')" :class="['button', `button-color_${style}`]">
    <slot />
  </button>
</template>

<style scoped>
.button {
  border-radius: 8px;
  padding: 11px 20px;
  font-size: 14px;
  font-weight: 500;
  cursor: pointer;
  width: auto;
}

@media (max-width: 576px) {
  .button {
    width: 100%;
  }
}

.button-color_check {
  background: linear-gradient(227deg, rgba(190, 226, 224, 1) 100%, rgba(170, 206, 219, 1) 0%);
  border: 1px solid #aacedb;
  color: #394155;
  background-size: 200%;
  background-position: left;
  transition:
    background-position 0.7s ease,
    color 0.7s ease;
}
.button-color_check:hover {
  background: #36a8a0;
  background-position: right;
  color: #ffffff;
}

.button-color_write {
  background: linear-gradient(227deg, rgba(23, 134, 172, 1) 0%, rgba(60, 185, 160, 1) 100%);
  color: #ffffff;
  border: transparent;
  background-size: 200%;
  background-position: left;
  transition: background-position 0.7s ease;
}
.button-color_write:hover {
  background-position: right;
}
</style>
