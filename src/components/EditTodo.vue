<script setup lang="ts">
import { defineEmits } from "vue";
// const defineProps<{todo:{done:boolean; content: string}}>();
const emit = defineEmits<{
  (event: "closeModal"): void;
}>();
</script>

<template>
  <div class="modal">
    <div class="overlay" @click="emit('closeModal')"></div>
    <div class="modal-card">
      <slot />
    </div>
  </div>
</template>

<style scoped></style>
