<script lang="ts" setup>
interface Props {
  variant: string
}
const { variant } = defineProps<Props>()

defineEmits(['click'])
</script>

<template>
  <button @click="$emit('click')" :class="['button', `button-color_${variant}`]">
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

.button-color_secondary {
  background: linear-gradient(227deg, rgba(190, 226, 224, 1) 100%, rgba(170, 206, 219, 1) 0%);
  border: 1px solid #aacedb;
  color: #394155;
  background-size: 200%;
  background-position: left;
  transition:
    background-position 0.7s ease,
    color 0.7s ease;
}
.button-color_secondary:hover {
  background: #36a8a0;
  background-position: right;
  color: #ffffff;
}

.button-color_primary {
  background: linear-gradient(227deg, rgba(23, 134, 172, 1) 0%, rgba(60, 185, 160, 1) 100%);
  color: #ffffff;
  border: transparent;
  background-size: 200%;
  background-position: left;
  transition: background-position 0.7s ease;
}
.button-color_primary:hover {
  background-position: right;
}
</style>
