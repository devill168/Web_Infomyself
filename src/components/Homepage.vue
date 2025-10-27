<template>
  <div class="container-fluid py-5 section-1">
    <div class="row align-items-center">
      <!-- Left Section: Personal Image -->
      <div class="col-12 col-md-6 text-center position-relative">
        <div class="flag-bg"></div>
        <img src="/img/personal.png" class="img-fluid personal-photo" />
      </div>

      <!-- Right Section: Text -->
      <div class="section1-MainText px-4 col-12 col-md-6 text-center text-md-start">
        <h3 class="text-light mb-2 title-section1" >{{ currentLanguage=== "KH"?"សួស្តីអ្នកទាំងអស់.! ខ្ញុំបាទឈ្មោះ" : "Hello everyone, my name is"}}</h3>
        <h1 class="fw-bold myname-section1">{{ currentLanguage ==="KH"? "រ៉ន ហ្សានី" : "Ran Sany" }}</h1>
       <h4 class="text-light mb-4 typing"> {{ currentLanguage==="KH"? "ខ្ញុំគឺជា" : "I'm a" }}
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
  </div>
</template>

<script setup lang="js">

import { ref, watch, onMounted } from "vue";
import { currentLanguage } from "../stores/languageStore.js"; // your global reactive var

// Define the two text versions
const fullTextEN = "Front-End Developer";
const fullTextKH = "មន្ត្រីផ្នែកអភិវឌ្ឈន៍ប្រព័ន្ធទិន្នន័យ";

const displayedText = ref("");
let index = 0;
let typingSpeed = 100; // milliseconds per character
let deleting = false;
let typingTimeout = null; // to clear timeout when language changes

// Function to select text based on language
const getFullText = () => {
  return currentLanguage.value === "KH" ? fullTextKH : fullTextEN;
};

// Typing animation
const typeText = () => {
  const fullText = getFullText();

  if (!deleting && index < fullText.length) {
    // Typing forward
    displayedText.value += fullText[index];
    index++;
    typingTimeout = setTimeout(typeText, typingSpeed);
  } else if (!deleting && index === fullText.length) {
    // Wait 2s before deleting
    deleting = true;
    typingTimeout = setTimeout(typeText, 3000);
  } else if (deleting && index > 0) {
    // Deleting backward
    displayedText.value = fullText.substring(0, index - 1);
    index--;
    typingTimeout = setTimeout(typeText, typingSpeed / 2);
  } else if (deleting && index === 0) {
    // Restart typing
    deleting = false;
    typingTimeout = setTimeout(typeText, typingSpeed);
  }
};

// Start typing on mount
onMounted(() => {
  typeText();
});

// Watch for language change → restart animation
watch(currentLanguage, () => {
  clearTimeout(typingTimeout);
  displayedText.value = "";
  index = 0;
  deleting = false;
  typeText();
});
</script>

<style scoped>
/* Flag as background layer */
.flag-bg {
  background: url("/img/cambodia-flag.webp") center center/cover no-repeat;
  position: absolute;
  inset: 0;
  opacity: 0.15; /* adjust visibility */
  z-index: 1;
}

/* Personal image above the flag */
.personal-photo {
  position: relative;
  z-index: 1000;
  max-width: 80%;
}

.title-section1{
  font-family: "Khmer OS Muol Light";
}
.myname-section1{
  margin-top: 5%;
  font-family: "Khmer OS Battambang";
  color:#feb47b;
}
.typing {
  margin-top: 3%;
  font-size: 18px;
  font-family: "Khmer OS Muol Light";
  padding-right: 5px;
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
  .personal-photo{
    z-index: 1;
  }
}
</style>
