<template>
  <div class="container py-5">
    <div class="experience">
      <h1>Experience Page</h1>
      <p>
        {{ message }}
      </p>
    </div>
  </div>
</template>

<script setup>
import { computed } from "vue";
import { currentLanguage } from "../stores/languageStore.js"; // ✅ fixed path

const message = computed(() => {
  return currentLanguage.value === "KH"
    ? "សូមស្វាគមន៍មកដល់គេហទំព័ររបស់យើងខ្ញុំ"
    : "Welcome to the experience.";
});
</script>

<style scoped>
@media (max-width: 991px) {
  .experience {
    margin-top: 10%;
  }
}
</style>
