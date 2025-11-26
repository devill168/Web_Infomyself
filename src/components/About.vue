<template>
  <div class="container py-5">

    <!-- SECTION 1 -->
    <section class="section-1" ref="section1">
      <div class="text-center">
        <div class="title-wrapper">
          <h1 class="title">
            {{ currentLanguage === "KH" ? "អំពីខ្ញុំ" : "About Me" }}
          </h1>
          <div class="title-border"></div>
        </div>
        

        <p class="subtitle">
          {{
            currentLanguage === "KH"
              ? "អ្នកអភិវឌ្ឍន៍មានភាពច្នៃប្រឌិត និងមានចិត្តស្ងប់ បង្កើតដំណើរឌីជីថលដ៏អស្ចារ្យ"
              : "A calm-minded creative developer crafting serene digital journeys"
          }}
        </p>
      </div>
    </section>

    <!-- SECTION 2 -->
    <section class="section-2" ref="section2">
      <div class="content-wrapper">
        
        <!-- TEXT -->
        <div class="text-content">
          <h2 class="greeting" @mouseenter="handleTextHover" @mouseleave="handleTextLeave">
            {{
              currentLanguage === "KH"
                ? "សួស្តី ខ្ញុំឈ្មោះ អ៊ុង សេរីរ័ត្ន — ជាគ្រូនគរបាលជាតិ, អភិវឌ្ឍន៍គេហទំព័រ Full Stack និងកម្មវិធីទូរស័ព្ទ, រចនា UI/UX, វិភាគមូលដ្ឋានទិន្នន័យ, និងអ្នកស្រាវជ្រាវ។"
                : "Hi, I’m Ung Sereyrath — a National Police Instructor, Full Stack Web Developer, Mobile App Developer, UI/UX Designer, Database Analyst, and Researcher."
            }}
          </h2>

          <p class="description" @mouseenter="handleTextHover" @mouseleave="handleTextLeave">
            {{
              currentLanguage === "KH"
                ? "ខ្ញុំមានចំណង់ចំណូលចិត្ត ក្នុងការបង្កើតបទពិសោធន៍ឌីជីថលឆ្លាតវៃ និងផ្តោតលើអ្នកប្រើប្រាស់ ថែមទាំងចែករំលែកចំណេះដឹង ជំរុញវឌ្ឍនភាព និងនវានុវត្តន៍។ បទពិសោធន៍របស់ខ្ញុំ មានទាំងផ្នែកអនុវត្តច្បាប់ និងបច្ចេកវិទ្យា ដែលផ្តល់ឱ្យខ្ញុំនូវទស្សនៈពិសេសមួយ — រួមទាំងវិន័យ ការគិតបែបទំនើប និងការដោះស្រាយបញ្ហា ដែលមានទិន្នន័យជាមូលដ្ឋាន។"
                : "I’m passionate about creating smart, user-focused digital experiences while sharing knowledge that drives progress and innovation. My background in both law enforcement and technology gives me a unique perspective—blending discipline, design thinking, and data-driven problem solving."
            }}
          </p>

          <h5 class="highlight" @mouseenter="handleTextHover" @mouseleave="handleTextLeave">
            {{
              currentLanguage === "KH"
                ? "ចេញពីការរចនាដែលមានភាពទាក់ទាញ និងការអភិវឌ្ឍកម្មវិធីគេហទំព័រ កម្មវិធីទូរស័ព្ទ រហូតដល់ការវិភាគទិន្នន័យ និងការធ្វើការស្រាវជ្រាវ ខ្ញុំខិតខំភ្ជាប់ភាពច្នៃប្រឌិតដែលមានគោលបំណងច្បាស់លាស់ — នឹងប្រែក្លាយគំនិតទៅជាលទ្ធផល ដែលមានឥទ្ធិពលដល់បុគ្គល និងអង្គការថែមទៀត។"
                : "From designing intuitive interfaces and developing web/mobile applications to analyzing data and conducting research, I focus on turning ideas into meaningful, impactful results that empower people and organizations."
            }}
          </h5>
        </div>

        <!-- IMAGE -->
        <div class="image-content">
          <div class="image-container" @mouseenter="startImageFloat" @mouseleave="stopImageFloat">
            <div class="image-wrapper">
              <img src="/img/back-flag cambodia.jpg" alt="Cambodia Flag" />
              <div class="image-overlay">
                <div class="overlay-content">
                  <span class="overlay-text">
                    {{ currentLanguage === "KH" ? "កម្ពុជា" : "Cambodia" }}
                  </span>
                </div>
              </div>
            </div>

            <div class="floating-elements">
              <div class="floating-element element-1">🇰🇭</div>
              <div class="floating-element element-2">✨</div>
              <div class="floating-element element-3">🌟</div>
            </div>
          </div>
        </div>

      </div>
    </section>

    <!-- SECTION 3 — TIMELINE -->
    <section class="section-3" ref="section3">
      <div class="timeline">
        <div
          class="timeline-item"
          v-for="(item, index) in translatedTimeline"
          :key="index"
          :class="{ 'timeline-item-hover': hoveredTimeline === index }"
          @mouseenter="() => handleTimelineHover(index)"
          @mouseleave="() => handleTimelineLeave(index)"
        >
          <div class="year">{{ item.year }}</div>
          <div class="content">
            <h3>{{ item.title }}</h3>
            <p>{{ item.description }}</p>
            <div class="timeline-connector"></div>
          </div>
        </div>
      </div>
    </section>

    <!-- SECTION 4 — QUOTE -->
    <section class="section-4" ref="section4">
      <div class="quote-container" @mouseenter="startQuotePulse" @mouseleave="stopQuotePulse">
        <h1 class="quote">
          {{
            currentLanguage === "KH"
              ? "ការកសាងបទពិសោធន៍ល្អ និងមានតម្លៃ ការគិតគូរយ៉ាងល្អិតល្អន់ និងការរចនាដ៏ស្ងប់ស្ងាត់បែបទំនើប"
              : "Building clean and meaningful experiences through thoughtful code and quiet design."
          }}
        </h1>

        <div class="quote-signature">
          — {{ currentLanguage === "KH" ? "រ៉ន ហ្សានី" : "RAN SANY" }}
           <svg class="signature-svg" viewBox="0 0 300 80">
             <path
                class="signature-path"
                d="M20 60 Q 80 10, 140 55 T 300 50"
                stroke="#d1d1d1"
                stroke-width="3"
                fill="none"
                stroke-linecap="round"
                stroke-linejoin="round"
              />
            </svg>
        </div>
      </div>
    </section>

      <!-- SECTION 5 — HOBBIES & INTERESTS -->
  <section class="section-5" ref="section5">
    <div class="section-header">
      <h1 class="title">
        {{ currentLanguage === "KH" ? "ចំណង់ចំណូលចិត្ត និងចំណាប់អារម្មណ៍" : "Hobbies & Interests" }}
      </h1>
      <div class="title-border"></div>
      <p class="section-description">
        {{
          currentLanguage === "KH"
            ? "នៅពេលដែលខ្ញុំមិនសរសេរកូដ ខ្ញុំរីករាយនឹងការស្វែងរកចំណង់ចំណូលចិត្តផ្សេងៗ ដែលជួយខ្ញុំរក្សារបៀបរស់នៅប្រកបដោយតុល្យភាព និងបន្តការសិក្សា"
            : "When I'm not coding, I enjoy pursuing various hobbies that help me maintain a balanced lifestyle and continue learning."
        }}
      </p>
    </div>

    <div class="hobbies-grid">
      <div
        class="hobby-card"
        v-for="(hobby, index) in translatedHobbies"
        :key="index"
        :class="{ 'card-hover': hoveredCard === index }"
        @mouseenter="() => handleCardHover(index)"
        @mouseleave="() => handleCardLeave(index)"
        :style="{ animationDelay: `${index * 0.1}s` }"
      >
        <div class="card-icon-wrapper">
          <div class="icon-background"></div>
          <div class="card-icon">
            {{ hobby.icon }}
          </div>
          <div class="icon-sparkle"></div>
        </div>
        <h3 class="card-title">{{ hobby.title }}</h3>
        <p class="card-description">{{ hobby.description }}</p>
        <div class="card-hover-effect"></div>
        <div class="card-glow"></div>
      </div>
    </div>
  </section>

  </div>
</template>



<script setup>
import { ref, onMounted, onUnmounted, computed } from "vue";
import { currentLanguage } from "../stores/languageStore.js";

const section1 = ref(null)
const section2 = ref(null)
const section3 = ref(null)
const section4 = ref(null)
const section5 = ref(null);

const hoveredTimeline = ref(null)
const isImageFloating = ref(false)
const isQuotePulsing = ref(false)
const hoveredCard = ref(null);

/* KH Timeline */
const timelineItems = ref([
  { year: '២០០៥', title: 'វិទ្យាល័យ', description: 'វិទ្យាល័យសន្ធរម៉ុក រាជធានីភ្នំពេញ' },
  { year: '២០១០', title: 'បរិញ្ញាបត្រ ព័ត៌មានវិទ្យា', description: 'សាកលវិទ្យាល័យមេគង្គកម្ពុជា រាជធានីភ្នំពេញ' },
  { year: '២០១១', title: 'បរិញ្ញាបត្រ អង់គ្លេស', description: 'សាកលវិទ្យាល័យគ្រប់គ្រងជាតិ រាជធានីភ្នំពេញ' },
  { year: '២០១៣', title: 'បរិញ្ញាបត្រជាន់ខ្ពស់ ព័ត៌មានវិទ្យា', description: 'សាកលវិទ្យាល័យន័រតុន រាជធានីភ្នំពេញ' },
  { year: '២០១០', title: 'ការគ្រប់គ្រងទិន្នន័យ', description: 'B.N.Consult - ក្រុមហ៊ុនប្រឹក្សាអភិវឌ្ឍកម្មវិធី/ប្រមូលទិន្នន័យ' },
  { year: '២០១៣', title: 'ការអភិវឌ្ឍប្រព័ន្ធ', description: 'B.N.Consult - ក្រុមហ៊ុនអភិវឌ្ឍកម្មវិធី' },
  { year: '២០១៧', title: 'Freelance', description: 'អ្នកអភិវឌ្ឍប្រព័ន្ធឯករាជ្យ' },
  { year: '២០២០', title: 'គ្រូនគរបាលជាតិ', description: 'សាលាបណ្តុះបណ្តាល នគរបាលជាតិ' },
]);

/* EN Timeline */
const timelineItemsEN = [
  { year: '2005', title: 'High School', description: 'SANTONMOK High School, Phnom Penh' },
  { year: '2010', title: 'B.A. in IT', description: 'Cambodian Mekong University, Phnom Penh' },
  { year: '2011', title: 'B.A. in English', description: 'National University of Management, Phnom Penh' },
  { year: '2013', title: 'Master in IT', description: 'Norton University, Phnom Penh' },
  { year: '2010', title: 'Data Management', description: 'B.N.Consult — Data & system development consulting' },
  { year: '2013', title: 'System Development', description: 'B.N.Consult — System development team' },
  { year: '2017', title: 'Freelance Developer', description: 'Independent system developer for various clients' },
  { year: '2020', title: 'National Police Instructor', description: 'Training School for the National Police of Cambodia' }
];

/* KH Hobbies */
const hobbiesKH = [
  {
    title: "ដំណើរកំសាន្ត និងធម្មជាតិ",
    description: "ការដើរកំសាន្តតាមរមណីដ្ឋានធម្មជាតិ ជាមួយសប្បាយរីករាយជាមួយធម្មជាតិស្រស់បំព្រង",
    icon: "🏞️"
  },
  {
    title: "ការអាន",
    description: "ចាប់អារម្មណ៍ដោយសៀវភៅវិទ្យាសាស្ត្រ និងបច្ចេកវិទ្យា។ ឥឡូវនេះកំពុងអាន 'បញ្ហារាងកាយបី'",
    icon: "📚"
  },
  {
    title: "តន្ត្រី",
    description: "ការស្តាប់ចំរៀងជួយអោយអារម្មណ៍ស្រស់ស្រាយនិងសប្បាយរីករាយជាមួយបទចម្រៀង",
    icon: "🎵"
  },
  {
    title: "កីឡា",
    description: "កីឡាបាល់ទាត់ និងការរត់ចំងាយជាចំណូលចិត្តតាំងពីកុមារ លេងកីឡាដើម្បីសុខភាព",
    icon: "⚽"
  },
  {
    title: "ការចុះកម្មវិធី",
    description: "ចូលចិត្តការចុះកម្មវិធីថ្មីៗ និងស្វែងយល់ពីបច្ចេកវិទ្យាដែលកំពុងអភិវឌ្ឍ",
    icon: "💻"
  },
  {
    title: "ការសរសេរ",
    description: "ការសរសេរកំណត់ត្រា អត្ថបទបច្ចេកទេស និងចំណេះដឹងផ្សេងៗដែលបានរៀន",
    icon: "✍️"
  },
];

/* EN Hobbies */
const hobbiesEN = [
  {
    title: "Travel & Nature",
    description: "Hiking in natural resorts with fun and fresh nature",
    icon: "🏞️"
  },
  {
    title: "Reading Book",
    description: "Fascinated by sci-fi and technology books. Currently reading 'The Three-Body Problem'.",
    icon: "📚"
  },
  {
    title: "Listening Song",
    description: "Listening to music helps to relax and feel happy with the music.",
    icon: "🎵"
  },
  {
    title: "Sports",
    description: "Football and long-distance running have been hobbies since childhood. Playing sports for health.",
    icon: "⚽"
  },
  {
    title: "Programming",
    description: "Enjoy exploring new technologies and programming languages in my free time.",
    icon: "💻"
  },
  {
    title: "Writing",
    description: "Writing technical articles, personal notes, and documenting knowledge I've acquired.",
    icon: "✍️"
  },
];

/* Computed Timeline */
const translatedTimeline = computed(() =>
  currentLanguage.value === "KH" ? timelineItems.value : timelineItemsEN
);
/* Computed Hobbies */
const translatedHobbies = computed(() =>
  currentLanguage.value === "KH" ? hobbiesKH : hobbiesEN
);

/* Card hover effects */
const handleCardHover = (index) => {
  hoveredCard.value = index;
};

const handleCardLeave = (index) => {
  hoveredCard.value = null;
};

/* Intersection Observer */
onMounted(() => {
  const observer = new IntersectionObserver(
    (entries) => {
      entries.forEach((entry) => {
        if (entry.isIntersecting) {
          entry.target.classList.add("animate-in");
        }
      });
    },
    { threshold: 0.1 }
  );

  if (section5.value) observer.observe(section5.value);
});


/* Intersection Observer */
onMounted(() => {
  const observer = new IntersectionObserver(
    (entries) => {
      entries.forEach((entry) => {
        if (entry.isIntersecting) {
          entry.target.classList.add("animate-in");
        }
      });
    },
    { threshold: 0.1 }
  );

  if (section5.value) observer.observe(section5.value);
});

/* Hover effects */
const handleTextHover = (e) => {
  e.target.style.transform = "translateY(-2px)";
  e.target.style.transition = "0.3s ease";
};
const handleTextLeave = (e) => {
  e.target.style.transform = "translateY(0)";
};
const handleTimelineHover = (i) => (hoveredTimeline.value = i);
const handleTimelineLeave = () => (hoveredTimeline.value = null);

/* Image + Quote hover */
const startImageFloat = () => (isImageFloating.value = true);
const stopImageFloat = () => (isImageFloating.value = false);
const startQuotePulse = () => (isQuotePulsing.value = true);
const stopQuotePulse = () => (isQuotePulsing.value = false);

/* Intersection Observer */
let observer;
onMounted(() => {
  observer = new IntersectionObserver(
    (entries) => {
      entries.forEach((entry) => {
        if (entry.isIntersecting) {
          entry.target.classList.add("animate-in");
        }
      });
    },
    { threshold: 0.1 }
  );

  [section1.value, section2.value, section3.value, section4.value].forEach((el) => {
    if (el) observer.observe(el);
  });
});
onUnmounted(() => observer && observer.disconnect());
</script>


<style scoped>
.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 20px;
}

/* Section 1 Styles - Typewriter Effect */
.section-1 {
  padding: 100px 0;
  text-align: center;
  opacity: 0;
  transform: translateY(50px);
  transition: all 1s cubic-bezier(0.4, 0, 0.2, 1);
  position: relative;
  overflow: hidden;
}

.section-1::before {
  content: '';
  position: absolute;
  top: 0;
  left: -100%;
  width: 100%;
  height: 100%;
  background: linear-gradient(90deg, transparent, rgba(52, 152, 219, 0.1), transparent);
  transition: left 1.5s ease;
}

.section-1.animate-in {
  opacity: 1;
  transform: translateY(0);
}

.section-1.animate-in::before {
  left: 100%;
}

.title-wrapper {
  display: inline-block;
  position: relative;
}

.title {
  font-size: 4rem;
  color: #2c3e50;
  margin-bottom: 10px;
  font-weight: 800;
  background: linear-gradient(135deg, white, #d1d1d1, #2c3e50);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  opacity: 0;
  transform: scale(0.8);
  animation: titleReveal 1.2s ease forwards 0.5s;
}

.title-underline {
  width: 0;
  height: 4px;
  background: linear-gradient(90deg, #3498db, #2c3e50);
  margin: 0 auto 30px;
  border-radius: 2px;
  animation: underlineExpand 1s ease forwards 1s;
}

.subtitle {
  font-size: 1.3rem;
  color: #d1d1d1;
  max-width: 600px;
  margin: 0 auto;
  line-height: 1.6;
  opacity: 0;
  transform: translateY(20px);
  animation: subtitleReveal 1s ease forwards 1.2s;
}

@keyframes titleReveal {
  to {
    opacity: 1;
    transform: scale(1);
  }
}

@keyframes underlineExpand {
  to {
    width: 200px;
  }
}

@keyframes subtitleReveal {
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

/* Section 2 Styles - Slide and Bounce */
.section-2 {
  padding: 100px 0;
  opacity: 0;
  transform: translateX(-100px);
  transition: all 1s cubic-bezier(0.4, 0, 0.2, 1);
}

.section-2.animate-in {
  opacity: 1;
  transform: translateX(0);
}

.content-wrapper {
  display: flex;
  flex-wrap: wrap;
  gap: 60px;
  align-items: center;
}

.text-content {
  flex: 1;
  min-width: 300px;
}



.highlight:hover {
  color: #d1d1d1;
  background: linear-gradient(135deg, rgba(52, 152, 219, 0.05), rgba(155, 89, 182, 0.05));
  box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
  transform: translateY(-2px) scale(1.01);
}

.image-content {
  flex: 1;
  min-width: 300px;
  display: flex;
  justify-content: center;
}

.image-container {
  position: relative;
  width: 420px;
  height: 550px;
  border-radius: 15px;
  overflow: hidden;
  box-shadow: 0 20px 40px rgba(0, 0, 0, 0.15);
  transition: all 0.5s cubic-bezier(0.4, 0, 0.2, 1);
  cursor: pointer;
}

.image-container:hover {
  transform: translateY(-10px) scale(1.03);
  box-shadow: 0 30px 60px rgba(0, 0, 0, 0.25);
}

.image-wrapper {
  position: relative;
  width: 100%;
  height: 100%;
  overflow: hidden;
}

.image-container img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform 0.5s ease;
}

.image-container:hover img {
  transform: scale(1.1);
}

.image-overlay {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: linear-gradient(45deg, rgba(52, 152, 219, 0.7), rgba(155, 89, 182, 0.7));
  opacity: 0;
  transition: opacity 0.3s ease;
  display: flex;
  align-items: center;
  justify-content: center;
}

.image-container:hover .image-overlay {
  opacity: 1;
}

.overlay-content {
  text-align: center;
  transform: translateY(20px);
  transition: transform 0.3s ease;
}

.image-container:hover .overlay-content {
  transform: translateY(0);
}

.overlay-text {
  color: white;
  font-size: 2rem;
  font-weight: bold;
  text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.5);
}

.floating-elements {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  pointer-events: none;
}

.floating-element {
  position: absolute;
  font-size: 1.5rem;
  opacity: 0;
  transition: all 0.5s ease;
}

.element-1 { top: 10%; left: 20%; }
.element-2 { top: 30%; right: 15%; }
.element-3 { bottom: 20%; left: 50%; }

.image-container:hover .element-1 {
  opacity: 1;
  transform: translateY(-20px) rotate(360deg);
  transition-delay: 0.1s;
}

.image-container:hover .element-2 {
  opacity: 1;
  transform: translateY(-15px) rotate(-360deg);
  transition-delay: 0.3s;
}

.image-container:hover .element-3 {
  opacity: 1;
  transform: translateY(-25px) scale(1.5);
  transition-delay: 0.5s;
}

.greeting {
  font-family: "Khmer OS Muol Light";
  font-size: 1.8rem;
  color: whitesmoke;
  margin-bottom: 25px;
  line-height: 1.7;
}

.description {
  font-family: "Khmer OS Battambang";
  font-size: 1.1rem;
  color: #d1d1d1;
  line-height: 1.7;
  margin-bottom: 25px;
}

.highlight {
  font-family: "Khmer OS Battambang";
  font-size: 1rem;
  color: #2b3a49;
  line-height: 1.7;
  padding: 25px;
  background: linear-gradient(135deg, #f8f9fa, #e9ecef);
  border-left: 6px solid #3498db;
  border-radius: 0 10px 10px 0;
  box-shadow: 0 5px 15px rgba(0, 0, 0, 0.08);
}

/* Section 3 Styles - Staggered Timeline */
.section-3 {
  padding: 100px 0;
  opacity: 0;
  transform: translateY(50px);
  transition: all 1s ease;
}

.section-3.animate-in {
  opacity: 1;
  transform: translateY(0);
}

.timeline {
  position: relative;
  max-width: 900px;
  margin: 0 auto;
}

.timeline::before {
  content: '';
  position: absolute;
  left: 50%;
  transform: translateX(-50%);
  width: 4px;
  height: 100%;
  background: linear-gradient(to bottom, #3498db, #9b59b6);
  border-radius: 2px;
}

.timeline-item {
  font-family: "Khmer OS Battambang";
  display: flex;
  justify-content: flex-end;
  padding-right: 40px;
  position: relative;
  margin: 30px 0;
  width: 50%;
  opacity: 0;
  transform: translateX(-50px);
  transition: all 0.6s cubic-bezier(0.4, 0, 0.2, 1);
  animation: timelineSlideIn 0.8s ease forwards;
  cursor: pointer;
}

.timeline-item:nth-child(even) {
  align-self: flex-end;
  justify-content: flex-start;
  padding-left: 40px;
  padding-right: 0;
  transform: translateX(50px);
}

.timeline-item-hover {
  transform: translateX(-30px) !important;
  z-index: 10;
}

.timeline-item:nth-child(even).timeline-item-hover {
  transform: translateX(30px) !important;
}

.timeline-item::after {
  content: '';
  position: absolute;
  width: 24px;
  height: 24px;
  right: -12px;
  background: white;
  border: 4px solid #3498db;
  top: 20px;
  border-radius: 50%;
  z-index: 2;
  transition: all 0.3s ease;
  box-shadow: 0 0 0 rgba(52, 152, 219, 0.4);
}

.timeline-item:hover::after {
  transform: scale(1.3);
  box-shadow: 0 0 20px rgba(52, 152, 219, 0.6);
  background: #3498db;
}

.timeline-item:nth-child(even)::after {
  left: -12px;
  right: auto;
}

.year {
  position: absolute;
  top: 20px;
  right: -100px;
  font-weight: bold;
  color: #3498db;
  font-size: 1.3rem;
  background: white;
  padding: 5px 15px;
  border-radius: 20px;
  box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
  transition: all 0.3s ease;
  pointer-events: none; /* Prevent year from interfering with hover */
}

.timeline-item:hover .year {
  transform: scale(1.1);
  background: #3498db;
  color: white;
}

.timeline-item:nth-child(even) .year {
  left: -100px;
  right: auto;
}

.content {
  padding: 25px;
  background: white;
  border-radius: 12px;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
  width: 100%;
  transition: all 0.3s ease;
  position: relative;
  overflow: hidden;
}

.content::before {
  content: '';
  position: absolute;
  top: 0;
  left: -100%;
  width: 100%;
  height: 100%;
  background: linear-gradient(90deg, transparent, rgba(52, 152, 219, 0.1), transparent);
  transition: left 0.5s ease;
}

.timeline-item:hover .content::before {
  left: 100%;
}

.timeline-item:hover .content {
  transform: translateY(-5px);
  box-shadow: 0 20px 40px rgba(0, 0, 0, 0.15);
  background: linear-gradient(135deg, #ffffff, #f8f9fa);
}

.content h3 {
  margin-top: 0;
  color: #2c3e50;
  font-size: 1.3rem;
}

.content p {
  margin-bottom: 0;
  color: #7f8c8d;
  line-height: 1.5;
}

.timeline-connector {
  position: absolute;
  top: 50%;
  right: -20px;
  width: 20px;
  height: 2px;
  background: #3498db;
  transform: translateY(-50%);
  opacity: 0;
  transition: all 0.3s ease;
}

.timeline-item:hover .timeline-connector {
  opacity: 1;
  width: 40px;
}

.timeline-item:nth-child(even) .timeline-connector {
  left: -20px;
  right: auto;
}

@keyframes timelineSlideIn {
  to {
    opacity: 1;
    transform: translateX(0);
  }
}



/* Section 4 Styles - Pulse and Glow */
.section-4 {
  padding: 120px 0;
  opacity: 0;
  transform: scale(0.9);
  transition: all 1s cubic-bezier(0.4, 0, 0.2, 1);
}

.section-4.animate-in {
  opacity: 1;
  transform: scale(1);
}

.quote-container {
  max-width: 900px;
  margin: 0 auto;
  text-align: center;
  padding: 60px 40px;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  border-radius: 20px;
  color: white;
  box-shadow: 0 20px 60px rgba(0, 0, 0, 0.3);
  position: relative;
  overflow: hidden;
  cursor: pointer;
  transition: all 0.5s ease;
}

.quote-container:hover {
  transform: translateY(-10px);
  box-shadow: 0 30px 80px rgba(0, 0, 0, 0.4);
  background: linear-gradient(135deg, #764ba2 0%, #667eea 100%);
}

.quote-background {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  overflow: hidden;
}

.floating-shape {
  position: absolute;
  border-radius: 50%;
  background: rgba(255, 255, 255, 0.1);
  animation: float 6s ease-in-out infinite;
}

.shape-1 {
  width: 100px;
  height: 100px;
  top: 10%;
  left: 10%;
  animation-delay: 0s;
}

.shape-2 {
  width: 150px;
  height: 150px;
  bottom: 20%;
  right: 10%;
  animation-delay: 2s;
}

.shape-3 {
  width: 80px;
  height: 80px;
  top: 50%;
  left: 80%;
  animation-delay: 4s;
}

@keyframes float {
  0%, 100% { transform: translateY(0) rotate(0deg); }
  50% { transform: translateY(-20px) rotate(180deg); }
}

.quote {
  font-family: "Khmer OS Metal Chrieng";
  font-size: 2rem;
  line-height: 1.8;
  font-weight: 400;
  font-style: italic;
  margin-bottom: 20px;
  position: relative;
  z-index: 2;
  text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.3);
  transition: all 0.3s ease;
}

.quote-container:hover .quote {
  transform: scale(1.02);
  text-shadow: 4px 4px 8px rgba(0, 0, 0, 0.4);
}

.quote-signature {
  font-family: "Khmer OS Metal Chrieng";
  font-size: 1.2rem;
  font-weight: 300;
  opacity: 0.9;
  position: relative;
  z-index: 2;
  font-style: italic;
}

/* Signature SVG */
.signature-svg {
  width: 200px;
  margin: 8px auto 0 auto;
  display: block;
}

/* Smooth handwriting animation */
.signature-path {
  stroke-dasharray: 300;
  stroke-dashoffset: 300;
  animation: signature-draw 11s ease forwards;
  opacity: 0.85;
}


/* Section 5 Styles - Enhanced Animated Cards */
.section-5 {
  padding: 100px 0;
  opacity: 0;
  transform: translateY(50px);
  transition: all 1s cubic-bezier(0.4, 0, 0.2, 1);
  position: relative;
  overflow: hidden;
}

.section-5::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: 
    radial-gradient(circle at 20% 80%, rgba(52, 152, 219, 0.05) 0%, transparent 50%),
    radial-gradient(circle at 80% 20%, rgba(155, 89, 182, 0.05) 0%, transparent 50%);
  pointer-events: none;
}

.section-5.animate-in {
  opacity: 1;
  transform: translateY(0);
}

.section-header {
  text-align: center;
  margin-bottom: 80px;
  position: relative;
  z-index: 2;
}

.section-title {
  font-size: 3.5rem;
  color: #2c3e50;
  margin-bottom: 20px;
  font-weight: 800;
  background: linear-gradient(135deg, #2c3e50, #3498db, #9b59b6);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  background-size: 200% 200%;
  animation: gradientShift 4s ease infinite;
}

@keyframes gradientShift {
  0%, 100% { background-position: 0% 50%; }
  50% { background-position: 100% 50%; }
}

.title-border {
  width: 120px;
  height: 4px;
  background: linear-gradient(90deg, #3498db, #9b59b6, #3498db);
  margin: 0 auto 30px;
  border-radius: 4px;
  position: relative;
  overflow: hidden;
  background-size: 200% 100%;
  animation: borderFlow 3s ease infinite;
}

@keyframes borderFlow {
  0%, 100% { background-position: -200% 0; }
  50% { background-position: 200% 0; }
}

.section-description {
  font-size: 1.3rem;
  color: #5d6d7e;
  max-width: 800px;
  margin: 0 auto;
  line-height: 1.7;
  font-weight: 300;
}

.hobbies-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 35px;
  max-width: 1300px;
  margin: 0 auto;
  padding: 0 20px;
  position: relative;
  z-index: 2;
}

.hobby-card {
  background: linear-gradient(145deg, #ffffff, #f8f9fa);
  border-radius: 20px;
  padding: 40px 30px;
  box-shadow: 
    0 15px 35px rgba(0, 0, 0, 0.1),
    0 5px 15px rgba(0, 0, 0, 0.05),
    inset 0 1px 0 rgba(255, 255, 255, 0.8);
  transition: all 0.6s cubic-bezier(0.23, 1, 0.32, 1);
  position: relative;
  overflow: hidden;
  opacity: 0;
  transform: translateY(40px) rotateX(10deg);
  animation: cardEntrance 0.8s ease forwards;
  cursor: pointer;
  border: 1px solid rgba(255, 255, 255, 0.8);
}

.hobby-card::before {
  content: '';
  position: absolute;
  top: 0;
  left: -100%;
  width: 100%;
  height: 100%;
  background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.4), transparent);
  transition: left 0.8s ease;
}

.hobby-card:hover::before {
  left: 100%;
}

.hobby-card:hover {
  transform: translateY(-15px) rotateX(0deg) scale(1.03);
  box-shadow: 
    0 25px 50px rgba(0, 0, 0, 0.15),
    0 15px 30px rgba(0, 0, 0, 0.1),
    inset 0 1px 0 rgba(255, 255, 255, 0.9);
}

.card-hover {
  transform: translateY(-15px) rotateX(0deg) scale(1.05) !important;
  box-shadow: 
    0 30px 60px rgba(52, 152, 219, 0.2),
    0 20px 40px rgba(155, 89, 182, 0.15),
    inset 0 1px 0 rgba(255, 255, 255, 0.9) !important;
}

.card-icon-wrapper {
  position: relative;
  width: 80px;
  height: 80px;
  margin: 0 auto 25px;
  display: flex;
  align-items: center;
  justify-content: center;
}

.icon-background {
  position: absolute;
  width: 100%;
  height: 100%;
  background: linear-gradient(135deg, #3498db, #9b59b6);
  border-radius: 50%;
  opacity: 0.1;
  transition: all 0.5s ease;
  transform: scale(0.8);
}

.hobby-card:hover .icon-background {
  transform: scale(1.1);
  opacity: 0.15;
  animation: iconPulse 2s ease infinite;
}

@keyframes iconPulse {
  0%, 100% { transform: scale(1.1); }
  50% { transform: scale(1.2); }
}

.card-icon {
  font-size: 2.8rem;
  position: relative;
  z-index: 2;
  transition: all 0.5s cubic-bezier(0.34, 1.56, 0.64, 1);
  filter: grayscale(0.3);
  transform: scale(1) rotate(0deg);
}

.hobby-card:hover .card-icon {
  transform: scale(1.3) rotate(10deg);
  filter: grayscale(0);
  animation: iconFloat 3s ease-in-out infinite;
}

@keyframes iconFloat {
  0%, 100% { transform: scale(1.3) rotate(10deg) translateY(0); }
  50% { transform: scale(1.3) rotate(10deg) translateY(-5px); }
}

.icon-sparkle {
  position: absolute;
  top: -5px;
  right: -5px;
  width: 20px;
  height: 20px;
  background: #3498db;
  border-radius: 50%;
  opacity: 0;
  transform: scale(0);
  transition: all 0.4s ease;
  animation: sparkleTwinkle 2s ease infinite;
}

.hobby-card:hover .icon-sparkle {
  opacity: 1;
  transform: scale(1);
}

@keyframes sparkleTwinkle {
  0%, 100% { opacity: 1; transform: scale(1); }
  50% { opacity: 0.7; transform: scale(0.8); }
}

.card-title {
  font-family: "Khmer OS Muol Light";
  font-size: 1.5rem;
  color: #2c3e50;
  margin-bottom: 20px;
  line-height: 1.7;
  font-weight: 700;
  transition: all 0.4s ease;
  text-align: center;
  position: relative;
}

.card-title::after {
  content: '';
  position: absolute;
  bottom: -8px;
  left: 50%;
  transform: translateX(-50%);
  width: 0;
  height: 2px;
  background: linear-gradient(90deg, #3498db, #9b59b6);
  transition: width 0.4s ease;
}

.hobby-card:hover .card-title {
  color: #3498db;
  transform: translateY(-2px);
}

.hobby-card:hover .card-title::after {
  width: 60px;
}

.card-description {
  font-family: "Khmer OS Battambang";
  font-size: 1.05rem;
  color: #5d6d7e;
  line-height: 1.7;
  transition: all 0.4s ease;
  text-align: center;
  font-weight: 300;
}

.hobby-card:hover .card-description {
  color: #2c3e50;
  transform: translateY(-2px);
}

.card-hover-effect {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: linear-gradient(135deg, rgba(52, 152, 219, 0.03), rgba(155, 89, 182, 0.03));
  opacity: 0;
  transition: opacity 0.4s ease;
  border-radius: 20px;
}

.hobby-card:hover .card-hover-effect {
  opacity: 1;
}

.card-glow {
  position: absolute;
  top: -2px;
  left: -2px;
  right: -2px;
  bottom: -2px;
  background: linear-gradient(135deg, #3498db, #9b59b6, #3498db);
  border-radius: 22px;
  opacity: 0;
  transition: opacity 0.4s ease;
  z-index: -1;
  filter: blur(10px);
}

.hobby-card:hover .card-glow {
  opacity: 0.3;
  animation: glowPulse 2s ease-in-out infinite;
}

@keyframes glowPulse {
  0%, 100% { opacity: 0.3; }
  50% { opacity: 0.5; }
}

@keyframes cardEntrance {
  to {
    opacity: 1;
    transform: translateY(0) rotateX(0deg);
  }
}

/* Staggered animation for cards */
.hobby-card:nth-child(1) { animation-delay: 0.1s; }
.hobby-card:nth-child(2) { animation-delay: 0.2s; }
.hobby-card:nth-child(3) { animation-delay: 0.3s; }
.hobby-card:nth-child(4) { animation-delay: 0.4s; }
.hobby-card:nth-child(5) { animation-delay: 0.5s; }
.hobby-card:nth-child(6) { animation-delay: 0.6s; }
.hobby-card:nth-child(7) { animation-delay: 0.7s; }
.hobby-card:nth-child(8) { animation-delay: 0.8s; }

/* Responsive Design */
@media (max-width: 1200px) {
  .hobbies-grid {
    grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
    gap: 30px;
  }
}

@media (max-width: 768px) {
  .section-title {
    font-size: 2.5rem;
  }
  
  .section-description {
    font-size: 1.1rem;
    padding: 0 20px;
  }
  
  .hobbies-grid {
    grid-template-columns: repeat(auto-fit, minmax(260px, 1fr));
    gap: 25px;
    padding: 0 15px;
  }
  
  .hobby-card {
    padding: 30px 25px;
  }
  
  .card-icon-wrapper {
    width: 70px;
    height: 70px;
  }
  
  .card-icon {
    font-size: 2.5rem;
  }
}

@media (max-width: 480px) {
  .hobbies-grid {
    grid-template-columns: 1fr;
  }
  
  .section-5 {
    padding: 70px 0;
  }
  
  .section-title {
    font-size: 2rem;
  }
  
  .hobby-card {
    padding: 25px 20px;
  }
}




@keyframes signature-draw {
  from {
    stroke-dashoffset: 300;
    opacity: 0;
  }
  to {
    stroke-dashoffset: 0;
    opacity: 1;
  }
}
/* Responsive Design */
@media (max-width: 768px) {
  .content-wrapper {
    flex-direction: column;
  }
  
  .timeline::before {
    left: 31px;
  }
  
  .timeline-item {
    width: 100%;
    padding-left: 80px;
    padding-right: 25px;
  }
  
  .timeline-item:nth-child(even) {
    padding-left: 80px;
    padding-right: 25px;
  }
  
  .timeline-item::after {
    left: 21px;
    right: auto;
  }
  
  .timeline-item:nth-child(even)::after {
    left: 21px;
  }
  
  .year {
    left: -60px;
    right: auto;
  }
  
  .timeline-item:nth-child(even) .year {
    left: -60px;
  }
  
  .title {
    font-size: 2.8rem;
  }
  
  .quote {
    font-size: 1.6rem;
  }
  
  .image-container {
    width: 280px;
    height: 400px;
  }
}
</style>