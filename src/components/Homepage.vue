<template>
  <div class="container-fluid py-5 section-1">
    <div class="row align-items-center">
      <!-- Left Section: Personal Image -->
      <div class="col-12 col-md-6 text-center position-relative">
        <div class="flag-bg"></div>
        <img src="/img/personal.png" class="img-fluid personal-photo"
        />
      </div>

      <!-- Right Section: Text -->
      <div class="section1-MainText px-4 col-12 col-md-6 text-center text-md-start">
        <h3 class="text-light mb-2">Hello everyone, my name is</h3>
        <h1 class="text-warning fw-bold">Ran Sany</h1>
       <h4 class="text-light mb-4"> I'm a
        <span class="typing">{{ displayedText }}</span>
        <span class="cursor">|</span>
      </h4>
        <div class="d-flex justify-content-center justify-content-md-start gap-3 fs-5">
          <i class="bi bi-google"></i>
          <i class="bi bi-twitter-x"></i>
          <i class="bi bi-facebook"></i>
          <i class="bi bi-telegram"></i>
          <i class="bi bi-twitter"></i>
        </div>
      </div>
    </div>


    <!-- <p>
        {{
          currentLanguage === 'KH'
            ? 'សូមស្វាគមន៍មកដល់គេហទំព័ររបស់យើងខ្ញុំ'
            : 'Welcome to the homepage.'
        }}
      </p> -->
  </div>
</template>

<script setup>

import { ref, onMounted } from 'vue';

const fullText = "Front-End Developer";
const displayedText = ref("");

let index = 0;
let typingSpeed = 100; // ms per character

const typeText = () => {
  if (index < fullText.length) {
    displayedText.value += fullText[index];
    index++;
    setTimeout(typeText, typingSpeed);
  }
};

onMounted(() => {
  typeText();
});
import { currentLanguage } from "../stores/languageStore.js"; // Call Global Variable for use directly
</script>

<style scoped>

/* Flag as background layer */
.flag-bg {
  background: url("/img/cambodia-flag.webp") center center/cover no-repeat;
  position: absolute;
  inset: 0;
  opacity: 0.15; /* adjust visibility */
  z-index: 1
}

/* Personal image above the flag */
.personal-photo {
  position: relative;
  z-index: 1000;
  max-width: 80%;
}

.typing {
  font-weight: 500;
}

.cursor {
  display: inline-block;
  width: 1ch;
  animation: blink 0.8s steps(1) infinite;
}

@keyframes blink {
  0%, 50% { opacity: 1; }
  51%, 100% { opacity: 0; }
}

@media (max-width: 991px) {
  .section-1 {
    margin-top: 10%;
  }
  .section1-MainText{
    margin-top: 5%;
  }
}
</style>
