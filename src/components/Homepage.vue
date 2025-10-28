<template>
  <div class="container-fluid py-5 section-1 ">
    <!-- Section-1 -->
    <div class="row align-items-center ">
      <!-- Left Section: Personal Image -->
      <div class="col-12 col-md-6 text-center position-relative">
        <div class="flag-bg"></div>
        <img src="/img/personal.png" class="img-fluid personal-photo" />
      </div>

      <!-- Right Section: Text -->
      <div class="section1-MainText px-4 col-12 col-md-6 text-center text-md-start">
        <h3 class="text-light mb-2 title-section1">{{ currentLanguage === "KH" ? "សួស្តីអ្នកទាំងអស់.! ខ្ញុំបាទឈ្មោះ" :
          "Hello everyone, my name is" }}</h3>
        <h1 class="fw-bold myname-section1">{{ currentLanguage === "KH" ? "រ៉ន ហ្សានី" : "Ran Sany" }}</h1>
        <h4 class="text-light mb-4 typing"> {{ currentLanguage === "KH" ? "ខ្ញុំគឺជា" : "I'm a" }}
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

    <!-- Section-2 -->
    <div class="container my-5 section-2">
      <h2 class="text-center mb-5 title-section2">
        {{ currentLanguage === "KH" ? "ស្នាដៃចុងក្រោយ" : "Latest Work" }}
      </h2>

      <div ref="scrollContainer" class="scrolling-wrapper row flex-row flex-nowrap g-4 align-items-stretch">
        <!-- Section2  Card 1 -->
        <div class="col-12 col-sm-6 col-md-6 col-lg-4 col-xl-4">
          <div class="card card-section2 shadow-sm h-100">
            <img
              src="https://cdn.prod.website-files.com/619e15d781b21202de206fb5/642e5f92f6147ed845692f97_How-Mobile-App-Testing-Makes-or-Breaks-Mobile-User-Experience.webp"
              class="cardSection2-img-top img-fluid">
            <div class="cardSection2-body">
              <h5 class="cardSection2-title">Project Title 1</h5>
              <p class="cardSection2-text">A short description of your project or work sample goes here.</p>
              <a href="#" class="btn btn-primary btn-section2">View More</a>
            </div>
          </div>
        </div>

        <!-- Section2 Card 2 -->
        <div class="col-12 col-sm-6 col-md-6 col-lg-4 col-xl-4">
          <div class="card card-section2 shadow-sm h-100">
            <img
              src="https://s3-figma-hubfile-images-production.figma.com/hub/file/carousel/img/50fbf02187ca0d4b2c2ae3a27e02d52ba9fbbf74"
              class="cardSection2-img-top img-fluid">
            <div class="cardSection2-body">
              <h5 class="cardSection2-title">Project Title 2</h5>
              <p class="cardSection2-text">A short description of your project or work sample goes here.</p>
              <a href="#" class="btn btn-primary btn-section2">View More</a>
            </div>
          </div>
        </div>

        <!-- Section2 Card 3  -->
        <div class="col-12 col-sm-6 col-md-6 col-lg-4 col-xl-4">
          <div class="card card-section2 shadow-sm h-100">
            <img src="/img/web_pseronal.png" class="cardSection2-img-top img-fluid">
            <div class="cardSection2-body">
              <h5 class="cardSection2-title">Project Title 3</h5>
              <p class="cardSection2-text">A short description of your project or work sample goes here.</p>
              <a href="#" class="btn btn-primary btn-section2">View More</a>
            </div>
          </div>
        </div>
      </div>
      <div class="dots-wrapper d-flex justify-content-center mt-3 d-lg-none d-xl-none">
        <span v-for="(card, idx) in 3" :key="idx" :class="['dot', activeDot === idx ? 'active' : '']"></span>
      </div>
    </div>


    <!-- Section-3 -->
   <div class="container box-section3 my-5 section-3">
  <h2 class="text-end mb-5 title-section3">
    {{ currentLanguage === "KH" ? "សូចនាករ ជំនាញ" : "Skill Indicator" }}
  </h2>

  <img src="/img/saky.png" class="img-fluid cardSection3-img" />

  <div class="row py-3 bg-light">
  <div v-for="(skill, index) in skills" :key="index" class="col-12 col-sm-6 col-md-4 col-lg-3 py-3" ref="skillCards">
    <div class="card h-100 text-center shadow-sm border-0">
      <div class="card-title">{{ skill.title }}</div>
      <div class="card-body">
        <h5 class="card-title mb-3">{{ skill.name }}</h5>
        <!-- Animated Progress Bar -->
        <div class="progress-container">
          <div class="progress-bar" :style="{ width: skill.currentLevel + '%' }"></div>
        </div>
        <!-- Animated Percentage -->
        <div class="percentage mt-2">{{ Math.floor(skill.currentLevel) }}%</div>
        </div>
    </div>
  </div>
</div>

</div>
  </div>
</template>

<script setup lang="js">

import { ref, watch, onMounted, nextTick } from "vue";
import { currentLanguage } from "../stores/languageStore.js"; // your global reactive var

// Define the two text versions
const fullTextEN = "Front-End Developer";
const fullTextKH = "មន្ត្រីផ្នែកអភិវឌ្ឈន៍ប្រព័ន្ធទិន្នន័យ";
const scrollContainer = ref(null);
const activeDot = ref(0);

const displayedText = ref("");
let index = 0;
let typingSpeed = 100; // milliseconds per character
let deleting = false;
let typingTimeout = null; // to clear timeout when language changes

// Skill data with progress levels
const skills = ref([
  {name: "C# Programming", level: 90, currentLevel: 0 },
  {name: "Vue.js / Front-End", level: 85, currentLevel: 0 },
  {name: "Database Design", level: 75, currentLevel: 0 },
  {name: "UI/UX Design", level: 70, currentLevel: 0 },
]);
const skillCards = ref([]);

// Animate progress bars when in view
const animateSkill = (skill) => {
  let start = 0;
  const end = skill.level;
  const duration = 1500; // 1.5 seconds
  const stepTime = 20; // 20ms per step
  const step = (end / duration) * stepTime;

  const interval = setInterval(() => {
    start += step;
    if (start >= end) {
      skill.currentLevel = end;
      clearInterval(interval);
    } else {
      skill.currentLevel = start;
    }
  }, stepTime);
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


//Animation Dot Dot Touch Scroll
const updateActiveDot = () => {
  const container = scrollContainer.value;
  if (!container) return;

  const scrollLeft = container.scrollLeft;
  const cardWidth =
    container.children[0].offsetWidth +
    parseInt(getComputedStyle(container.children[0]).marginRight);

  activeDot.value = Math.round(scrollLeft / cardWidth);
};

// Function to select text based on language
const getFullText = () => {
  return currentLanguage.value === "KH" ? fullTextKH : fullTextEN;
};

// Start typing on mount
onMounted( async() => {
  typeText();

    const container = scrollContainer.value;
  if (container) {
    container.addEventListener("scroll", updateActiveDot, { passive: true });
    container.addEventListener("touchmove", updateActiveDot, { passive: true });
  }
  await nextTick();
  // IntersectionObserver triggers animation when skill cards are visible
  const observer = new IntersectionObserver(
    (entries) => {
      entries.forEach((entry) => {
        if (entry.isIntersecting) {
          const idx = skillCards.value.indexOf(entry.target);
          if (idx !== -1) animateSkill(skills.value[idx]);
          observer.unobserve(entry.target); // animate only once
        }
      });
    },
    { threshold: 0.5 }
  );

  skillCards.value.forEach((card) => observer.observe(card));

  observeSkills();
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

/* --- Skill Progress Bar Styles --- */
.progress-container {
  width: 100%;
  height: 12px;
  background: #e9ecef;
  border-radius: 6px;
  overflow: hidden;
}

.progress-bar {
  height: 100%;
  width: 0;
  background: linear-gradient(90deg, #0d6efd, #6610f2);
  border-radius: 6px;
  transition: width 1.5s ease-out; /* smooth animation */
}

.percentage {
  font-weight: 600;
  color: #0d6efd;
  font-size: 0.95rem;
}

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
  z-index: 1;
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
.title-section2{
  font-family: "Khmer OS Muol Light";
}

 .card-section2 {
  position: relative;
  border: none;
  border-radius: 18px;
  overflow: hidden;
  background: white;
  backdrop-filter: blur(10px);
  box-shadow: 0 8px 20px rgba(0, 0, 0, 0.1);
  transition: all 0.4s ease;
}

.card-section2:hover {
  transform: translateY(-12px) scale(1.02);
  box-shadow: 0 20px 40px rgba(13, 110, 253, 0.25);
  cursor: pointer;
}

/* Card Image */
.cardSection2-img-top {
  width: 100%;
  height: 250px;
  object-fit: cover;
  transition: transform 0.6s ease, filter 0.6s ease;
}

.card-section2:hover .cardSection2-img-top {
  transform: scale(1.1);
  filter: brightness(0.9);
  cursor: pointer;
}

/* Gradient Overlay */
.card-section2::after {
  content: "";
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: linear-gradient(
    180deg,
    rgba(13, 110, 253, 0.15),
    rgba(13, 110, 253, 0)
  );
  opacity: 0;
  transition: opacity 0.4s ease;
  z-index: 1;
}

.card-section2:hover::after {
  opacity: 1;
}

/* Card Body */
.cardSection2-body {
  position: relative;
  z-index: 2;
  padding: 20px;
  background: transparent;
  transition: background 0.4s ease;
}

.cardSection2-title {
  font-weight: 700;
  font-size: 1.25rem;
  color: #0d6efd;
  margin-bottom: 10px;
}

.cardSection2-text {
  color: #555;
  font-size: 0.95rem;
  line-height: 1.6;
}

.cardSection3-img{
  width: 25%;
  height: 25%;
  display: block;
  margin: 0 auto; /* centers horizontally */
}


/* Make the row scrollable horizontally on medium screens */
.scrolling-wrapper {
  overflow-x: auto;
  overflow-y: hidden;
  -webkit-overflow-scrolling: touch; /* smooth scrolling on iOS */
  scroll-behavior: smooth;
  scroll-snap-type: x mandatory;
  -webkit-overflow-scrolling: touch;
}
.scrolling-wrapper > .col-12 {
  scroll-snap-align: start;
}

/* Hide scrollbar for aesthetics */
.scrolling-wrapper::-webkit-scrollbar {
  display: none;
}

/* Optional: Add some spacing at the end */
.scrolling-wrapper .col-12 {
  flex: 0 0 auto;
}

/* Button Styling */
.btn-section2 {
  background: linear-gradient(90deg, #da4d40 0%, #7a2828 100%);
  background-size: 200% auto; /* makes gradient larger for movement */
  border: none;
  font-weight: 600;
  border-radius: 8px;
  color: #fff;
  transition: all 0.5s ease;
  box-shadow: 0 2px 6px rgba(13, 110, 253, 0.2);
  background-position: left center; /* default position */
}

.btn-primary:hover {
  background-position: right center; /* moves gradient smoothly */
  transform: scale(1.05);
  box-shadow: 0 4px 15px rgba(13, 110, 253, 0.3);
}

.dots-wrapper {
  gap: 8px;
}

.dot {
  width: 10px;
  height: 10px;
  border-radius: 50%;
  background: #ccc;
  transition: background 0.3s;
}

.dot.active {
  background: #0d6efd;
}

.typing {
  margin-top: 3%;
  font-size: 18px;
  font-family: "Khmer OS Muol Light";
  font-weight: 500;
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
  .cardSection3-img{
  width: 50%;
  height: 50%;
  }
}

</style>
