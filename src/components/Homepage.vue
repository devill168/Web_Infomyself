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
        <div class="social-icons d-flex justify-content-center justify-content-md-start gap-3 fs-5">
          <i class="bi bi-google"></i>
          <i class="bi bi-twitter-x"></i>
          <i class="bi bi-facebook"></i>
          <i class="bi bi-telegram"></i>
          <i class="bi bi-twitter"></i>
        </div>
      </div>
    </div>


   <!-- Section-2 -->
  <div class="section-2">
    <div class="title-border "></div>
    <div class="container">
      <h2 class="section-title">{{ currentLanguage === "KH" ? "ស្នាដៃរបស់ចុងក្រោយខ្ញុំ" : "Our Lasted Projects" }}</h2>
      <p class="section-subtitle">{{ currentLanguage === "KH" ? "ដំណោះស្រាយជូនលោកអ្នកប្រកបដោយភាពច្នៃប្រឌិតដែលបង្កើតឡើងដោយបច្ចេកវិទ្យាទំនើប" : "Innovative software solutions built with modern technologies" }}</p>
      
      <div class="cards-container">
        <div 
          v-for="(card, index) in cards" 
          :key="card.id"
          class="card"
          :class="{ 'loading': isLoading }"
          :style="{ '--delay': index * 0.1 + 's' }"
        >
          <!-- Loading Skeleton -->
          <div v-if="isLoading" class="skeleton">
            <div class="skeleton-image"></div>
            <div class="skeleton-content">
              <div class="skeleton-title"></div>
              <div class="skeleton-description"></div>
              <div class="skeleton-footer"></div>
            </div>
          </div>
          
          <!-- Card Content -->
          <div v-else class="card-content">
            <div class="card-image">
              <img 
                :src="card.thumbnailUrl" 
                :alt="card.title" 
                loading="lazy"
                @error="(e) => handleImageError(e, card)"
              />
              <div class="card-overlay">
                <button class="view-btn" @click="viewProject(card)">
                  <i class="fas fa-external-link-alt"></i>
                  View Project
                </button>
              </div>
              <div class="card-shine"></div>
              <div class="project-badge">
                <span class="category-badge">{{ card.category }}</span>
              </div>
            </div>
            <div class="card-body">
              <h3 class="card-title">{{ formatTitle(card.title) }}</h3>
              <p class="card-description">{{ card.description }}</p>
              
              <!-- Tech Stack -->
              <div class="tech-stack">
                <span 
                  v-for="tech in card.techStack" 
                  :key="tech"
                  class="tech-tag"
                >
                  {{ tech }}
                </span>
              </div>
              
              <div class="card-footer">
                <div class="project-info">
                  <span 
                    class="status-badge"
                    :style="{ backgroundColor: getStatusColor(card.status) }"
                  >
                    {{ card.status }}
                  </span>
                </div>
                <button 
                  class="like-btn" 
                  @click="toggleLike(card.id)"
                  :class="{ 'liked': card.liked }"
                >
                  <i :class="['fas', 'fa-heart']"></i>
                  {{ card.liked ? 'Saved' : 'Save' }}
                </button>
              </div>
            </div>
            <div class="card-border"></div>
          </div>
        </div>
      </div>
      
      <!-- Error Message -->
      <div v-if="error && !isLoading" class="error-message">
        <i class="fas fa-exclamation-triangle"></i>
        <p>{{ error }}</p>
        <button @click="fetchData" class="retry-btn">
          <i class="fas fa-redo"></i>
          Try Again
        </button>
      </div>

      <!-- Loading more indicator -->
      <div v-if="isLoading" class="loading-indicator">
        <div class="spinner"></div>
        <p>Loading projects...</p>
      </div>
    </div>
  </div>






    <!-- Section-3 -->
    <div class="container box-section3 my-5 section-3">
      <h2 class="text-end mb-5 title-section3">
        {{ currentLanguage === "KH" ? "សូចនាករ ជំនាញ" : "Skill Indicator" }}
      </h2>

      <img src="/img/saky.png" class="img-fluid cardSection3-img" />

      <div class="row py-3 rounded-4  bg-white">
        <div v-for="(skill, index) in skills" :key="index" class="col-12 col-sm-6 col-md-4 col-lg-3 py-3"
          ref="skillCards">
          <div class="card h-100 text-center shadow-sm border-0">
            <div class="card-title fw-bold fs-5">{{ skill.title }}</div>
            <div class="card-body">
              <div v-for="(subSkill, i) in skill.items" :key="i" class="mb-4">
                <h6 class="card-subtitle mb-1">{{ subSkill.name }}</h6>
                <!-- Animated Progress Bar -->
                <div class="progress-container">
                  <div class="progress-bar" :style="{ width: subSkill.currentLevel + '%' }"></div>
                </div>
                <!-- Animated Percentage -->
                <div class="percentage mt-1">{{ Math.floor(subSkill.currentLevel) }}%</div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>


    <div class="container section-4">
      <h2 class="text-start mb-5 title-section4">{{ currentLanguage ==="KH"? "រចនាសម្ព័ន្ធក្នុងផ្នែកបច្ចុប្បន្ន" :
        "Organization Unit"}}</h2>

      <div class="chart-wrapper">
        <h3 class="text-center">MIS Unit</h3>
        <div id="chartDiv"></div>
      </div>
    </div>

  </div>
</template>

<script setup lang="js">

import { ref, watch, onMounted, nextTick } from "vue";
import { currentLanguage } from "../stores/languageStore.js"; // your global reactive var



const cards = ref([])
const isLoading = ref(true)
const error = ref(null)

// Real API URL - Using JSONPlaceholder photos API
const API_URL = 'https://jsonplaceholder.typicode.com/photos?_limit=3'

// Fetch data from API
const fetchData = async () => {
  try {
    isLoading.value = true
    error.value = null
    
    // Real API call
    const response = await fetch(API_URL)
    
    if (!response.ok) {
      throw new Error(`HTTP error! status: ${response.status}`)
    }
    
    const data = await response.json()
    
    // Custom titles and descriptions for software projects
    const customTitles = [
      "Smart POS Cloud",
      "Malaria Information System", 
      "Mobile App"
    ]
    
    const customDescriptions = [
      "Cloud-based Point of Sale system with real-time analytics and inventory management",
      "Comprehensive malaria tracking and prevention platform for healthcare providers",
      "Cross-platform mobile application with offline capabilities and push notifications"
    ]
     const customImages = [
      "https://cdn.prod.website-files.com/619e15d781b21202de206fb5/642e5f92f6147ed845692f97_How-Mobile-App-Testing-Makes-or-Breaks-Mobile-User-Experience.webp",
      "https://cdn.prod.website-files.com/633fda66cb2f195f7271913e/63b3eb8d19c92c7acc5028bc_Cloud-pos_main.png  ",
      "https://t4.ftcdn.net/jpg/02/83/46/33/360_F_283463385_mfnrx6RPU3BqObhVuVjYZjeZ5pegE7xq.jpg"
    ]

    // Custom project categories
    const projectCategories = ["Mobile App Solutions", "POS Systems", "Web Development"]
    
    // Transform API data with our custom content
    cards.value = data.map((item, index) => ({
      id: item.id,
      category: projectCategories[index] || "Project",
      title: customTitles[index] || item.title,
      description: customDescriptions[index] || item.title,
      // Use software/tech related images
      url: `https://images.unsplash.com/photo-1551288049-bebda4e38f71?ixlib=rb-4.0.3&w=600`, // Dashboard
      thumbnailUrl: customImages[index] || "Imagesx ",
      techStack: ["Vue.js", "Node.js", "MongoDB"],
      status: "Completed",
      liked: false
    }))
    
    console.log('Data successfully fetched from API:', API_URL)
    
  } catch (err) {
    error.value = `Failed to load projects from API. Please check your connection. Error: ${err.message}`
    console.error('Error fetching data from API:', err)
    
    // Fallback data with software project images
    cards.value = [
      {
        id: 1,
        category: "Business Solutions",
        title: "Smart POS Cloud",
        description: "Cloud-based Point of Sale system with real-time analytics and inventory management",
        url: "https://images.unsplash.com/photo-1551288049-bebda4e38f71?ixlib=rb-4.0.3&w=600", // Dashboard
        thumbnailUrl: "https://images.unsplash.com/photo-1551288049-bebda4e38f71?ixlib=rb-4.0.3&w=300",
        techStack: ["Vue.js", "Node.js", "MongoDB"],
        status: "Completed",
        liked: false
      },
      {
        id: 2,
        category: "Healthcare Systems",
        title: "Malaria Information System",
        description: "Comprehensive malaria tracking and prevention platform for healthcare providers",
        url: "https://images.unsplash.com/photo-1576091160399-112ba8d25d1f?ixlib=rb-4.0.3&w=600", // Healthcare
        thumbnailUrl: "https://images.unsplash.com/photo-1576091160399-112ba8d25d1f?ixlib=rb-4.0.3&w=300",
        techStack: ["React", "Python", "PostgreSQL"],
        status: "In Progress",
        liked: false
      },
      {
        id: 3,
        category: "Mobile Development",
        title: "Mobile App",
        description: "Cross-platform mobile application with offline capabilities and push notifications",
        url: "https://images.unsplash.com/photo-1512941937669-90a1b58e7e9c?ixlib=rb-4.0.3&w=600", // Mobile
        thumbnailUrl: "https://images.unsplash.com/photo-1512941937669-90a1b58e7e9c?ixlib=rb-4.0.3&w=300",
        techStack: ["React Native", "Firebase", "Redux"],
        status: "Completed",
        liked: false
      }
    ]
  } finally {
    isLoading.value = false
  }
}

// Format title to be shorter
const formatTitle = (title) => {
  const words = title.split(' ').slice(0, 3)
  return words.join(' ') + (title.split(' ').length > 3 ? '...' : '')
}

// Toggle like status
const toggleLike = (cardId) => {
  const card = cards.value.find(c => c.id === cardId)
  if (card) {
    card.liked = !card.liked
  }
}

// View project function
const viewProject = (card) => {
  console.log('Viewing project:', card.title)
  // In a real app, you might navigate to project details page
  window.open(card.url, '_blank')
}

// Improved image error handling
const handleImageError = (event, card) => {
  console.log('Image failed to load, using fallback:', card.title)
  event.target.src = `https://images.unsplash.com/photo-1551288049-bebda4e38f71?ixlib=rb-4.0.3&w=300` // Fallback to dashboard image
}

// Get status color
const getStatusColor = (status) => {
  const colors = {
    'Completed': '#10b981',
    'In Progress': '#f59e0b',
    'Planning': '#6366f1'
  }
  return colors[status] || '#6b7280'
}

// Fetch data when component mounts
onMounted(() => {
  fetchData()
})





const orgData = [
  {
    id: "1",
    parent: "",
    name: "Ngor Pengby",
    position: "Head Of Unit",
    phone: "0123456789",
    email: "john@example.com",
    address: "Phnom Penh",
    photo: "/img/Ngor_Pengby.png"
  },
  {
    id: "2",
    parent: "1",
    name: "Sok Kimleng",
    position: "Senior Developer",
    phone: "0987654321",
    email: "sara@example.com",
    address: "Phnom Penh",
    photo: "/img/Sok Kimleng.png"
  },
  {
    id: "3",
    parent: "1",
    name: "Yoem Rattana",
    position: "Senior Developer",
    phone: "0987654321",
    email: "sara@example.com",
    address: "Phnom Penh",
    photo: "/img/Yoem Rattana.png"
  },
    {
    id: "4",
    parent: "2",
    name: "Hem Vanna",
    position: "Designer & Coordinator Officer",
    phone: "0987654321",
    email: "sara@example.com",
    address: "Phnom Penh",
    photo: "/img/Hem Vanna.png"
  },
      {
    id: "5",
    parent: "2",
    name: "Ou Vunsokserey",
    position: "Data Analyzer Officer",
    phone: "0987654321",
    email: "sara@example.com",
    address: "Phnom Penh",
    photo: "/img/Ou Vunsokserey.png"
  },
      {
    id: "6",
    parent: "3",
    name: "Ran Sany",
    position: "Developer Officer",
    phone: "0987654321",
    email: "sara@example.com",
    address: "Phnom Penh",
    photo: "/img/Mr.Ran Sany.png"
  },
    {
    id: "7",
    parent: "3",
    name: "Soam Daroth",
    position: "Assistant Developer Officer",
    phone: "0987654321",
    email: "sara@example.com",
    address: "Phnom Penh",
    photo: "/img/Daroth.png"
  }
];

function makeSeries(data) {
  return [
    {
      points: data.map(item => ({
        id: item.id,
        parent: item.parent === "" ? null : item.parent,
        name: item.name,
        attributes: {
          position: item.position,
          phone: item.phone,
          email: item.email,
          address: item.address,
          photo: item.photo
        }
      }))
    }
  ];
}

onMounted(() => {
  const series = makeSeries(orgData);
  renderChart(series);
});

/* Render Chart */
function renderChart(series) {
  JSC.chart("chartDiv", {
    type: "organizational down",
    tooltip: { enabled: false }, // Disable tooltips

    defaultPoint: {
      tooltip: false, // No JSC tooltip
      title: "",      // No browser tooltip

      connectorLine: {
        width: 3,
        color: "#dcdcdc",
        animation: { duration: 600 }
      },

      annotation: {
        asHTML: true,
        padding: 4,
        label: {
          text: `
            <div class="nodeBox">
              <img class="zoomPhoto" src="%photo" width="110" height="120" />
              <div class="personDescription">
                <b>%position</b><br>
                %name
              </div>
            </div>
          `
        }
      }
    },

    animation: {
      duration: 600,
      type: "fadeInUp",
      easing: "easeOut"
    },

    series
  });
}





// Define the two text versions
const fullTextEN = "Front-End Developer";
const fullTextKH = "មន្ត្រីផ្នែកអភិវឌ្ឈន៍ប្រព័ន្ធទិន្នន័យ";

const displayedText = ref("");
let index = 0;
let typingSpeed = 100; // milliseconds per character
let deleting = false;
let typingTimeout = null; // to clear timeout when language changes

// Skill data with progress levels
const skills = ref([
  {
    title: "Programming",
    items: [
      { name: "C#", level: 90, currentLevel: 0 },
      { name: "Java", level: 85, currentLevel: 0 },
      { name: "Python", level: 80, currentLevel: 0 },
      { name: "VB.Net", level: 70, currentLevel: 0 },
    ],
  },
  {
    title: "Web Developer",
    items: [
      { name: "Vue.js", level: 95, currentLevel: 0 },
      { name: "React.js", level: 90, currentLevel: 0 },
      { name: "PHP", level: 85, currentLevel: 0 },
      { name: "Node.js", level: 75, currentLevel: 0 },
    ],
  },
  {
    title: "Database Design",
    items: [
      { name: "SQL Server", level: 88, currentLevel: 0 },
      { name: "MySQL", level: 85, currentLevel: 0 },
      { name: "MongoDB", level: 80, currentLevel: 0 },
      { name: "Firebase", level: 70, currentLevel: 0 },
    ],
  },
  {
    title: "UX/UI",
    items: [
      { name: "Adobe XD", level: 90, currentLevel: 0 },
      { name: "Figma", level: 85, currentLevel: 0 },
      { name: "Canvas", level: 75, currentLevel: 0 },
      { name: "Photoshop", level: 80, currentLevel: 0 },
    ],
  },
]);
const skillCards = ref([]);

// Animate progress bars when in view
const animateSkill = (subSkill) => {
  let start = 0;
  const end = subSkill.level;
  const duration = 1500;
  const stepTime = 20;
  const step = (end / duration) * stepTime;

  const interval = setInterval(() => {
    start += step;
    if (start >= end) {
      subSkill.currentLevel = end;
      clearInterval(interval);
    } else {
      subSkill.currentLevel = start;
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


// Function to select text based on language
const getFullText = () => {
  return currentLanguage.value === "KH" ? fullTextKH : fullTextEN;
};

// Start typing on mount
onMounted( async() => {
  typeText();


  await nextTick();

  // Observe each skill card
  const observer = new IntersectionObserver(
    (entries) => {
      entries.forEach((entry) => {
        if (entry.isIntersecting) {
          const idx = skillCards.value.indexOf(entry.target);
          if (idx !== -1) {
            skills.value[idx].items.forEach((sub) => animateSkill(sub));
          }
          observer.unobserve(entry.target); // Animate once
        }
      });
    },
    { threshold: 0.5 }
  );
  skillCards.value.forEach((card) => {
    if (card) observer.observe(card);
  });
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
.section-2 {
  padding: 4rem 0;
  min-height: 80vh;
}

.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 1rem;
}

.section-title {
  font-family: "Khmer OS Muol Light";
  text-align: center;
  margin-bottom: 1rem;
  color: whitesmoke;
  font-weight: 500;
  animation: titleGlow 3s ease-in-out infinite alternate;
}

.section-subtitle {
  text-align: center;
  font-family: "Khmer OS Battambang";
  color: #d1d1d1;
  margin-bottom: 3rem;
  font-size: 1rem;
  animation: fadeInUp 1s ease-out;
}

.cards-container {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(350px, 1fr));
  gap: 2rem;
  margin-bottom: 2rem;
}

.card {
  background: white;
  border-radius: 16px;
  overflow: hidden;
  box-shadow: 
    0 4px 20px rgba(0, 0, 0, 0.08),
    0 2px 8px rgba(0, 0, 0, 0.05);
  transition: all 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275);
  height: fit-content;
  position: relative;
  animation: cardEntrance 0.6s ease-out var(--delay) both;
  transform-style: preserve-3d;
  perspective: 1000px;
}

.card:hover {
  transform: 
    translateY(-12px) 
    rotateX(2deg) 
    rotateY(1deg)
    scale(1.02);
  box-shadow: 
    0 25px 50px rgba(0, 0, 0, 0.15),
    0 15px 30px rgba(0, 0, 0, 0.1),
    0 0 0 1px rgba(255, 255, 255, 0.1);
}

/* Project Badge */
.project-badge {
  position: absolute;
  top: 1rem;
  left: 1rem;
  z-index: 3;
}

.category-badge {
  background: rgba(102, 126, 234, 0.9);
  color: white;
  padding: 0.4rem 0.8rem;
  border-radius: 20px;
  font-size: 0.75rem;
  font-weight: 600;
  backdrop-filter: blur(10px);
}

/* Tech Stack */
.tech-stack {
  display: flex;
  flex-wrap: wrap;
  gap: 0.5rem;
  margin-bottom: 1rem;
}

.tech-tag {
  background: #f1f5f9;
  color: #475569;
  padding: 0.3rem 0.6rem;
  border-radius: 12px;
  font-size: 0.75rem;
  font-weight: 500;
  border: 1px solid #e2e8f0;
}

/* Status Badge */
.status-badge {
  color: white;
  padding: 0.3rem 0.8rem;
  border-radius: 12px;
  font-size: 0.75rem;
  font-weight: 600;
}

/* Rest of the CSS remains the same as previous code */
.card-border {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  border-radius: 16px;
  background: linear-gradient(135deg, 
    rgba(255,255,255,0.8) 0%, 
    rgba(255,255,255,0.2) 50%, 
    rgba(255,255,255,0.8) 100%);
  opacity: 0;
  transition: opacity 0.4s ease;
  pointer-events: none;
}

.card:hover .card-border {
  opacity: 1;
  animation: borderGlow 2s ease-in-out infinite;
}

/* Card Entrance Animation */
@keyframes cardEntrance {
  0% {
    opacity: 0;
    transform: translateY(50px) scale(0.9);
  }
  100% {
    opacity: 1;
    transform: translateY(0) scale(1);
  }
}

@keyframes titleGlow {
  0% {
    filter: drop-shadow(0 0 10px rgba(102, 126, 234, 0.3));
  }
  100% {
    filter: drop-shadow(0 0 20px rgba(102, 126, 234, 0.6));
  }
}

@keyframes borderGlow {
  0%, 100% {
    opacity: 0.5;
  }
  50% {
    opacity: 0.8;
  }
}

/* Skeleton Loading Styles */
.skeleton {
  padding: 0;
  animation: skeletonPulse 2s ease-in-out infinite;
}

.skeleton-image {
  height: 200px;
  background: linear-gradient(90deg, #f0f0f0 25%, #e0e0e0 50%, #f0f0f0 75%);
  background-size: 200% 100%;
  animation: loading 1.5s infinite;
}

.skeleton-content {
  padding: 1.5rem;
}

.skeleton-title {
  height: 20px;
  background: linear-gradient(90deg, #f0f0f0 25%, #e0e0e0 50%, #f0f0f0 75%);
  background-size: 200% 100%;
  animation: loading 1.5s infinite;
  border-radius: 4px;
  margin-bottom: 0.75rem;
  width: 70%;
}

.skeleton-description {
  height: 16px;
  background: linear-gradient(90deg, #f0f0f0 25%, #e0e0e0 50%, #f0f0f0 75%);
  background-size: 200% 100%;
  animation: loading 1.5s infinite;
  border-radius: 4px;
  margin-bottom: 1rem;
  width: 90%;
}

.skeleton-footer {
  height: 14px;
  background: linear-gradient(90deg, #f0f0f0 25%, #e0e0e0 50%, #f0f0f0 75%);
  background-size: 200% 100%;
  animation: loading 1.5s infinite;
  border-radius: 4px;
  width: 60%;
}

@keyframes loading {
  0% {
    background-position: 200% 0;
  }
  100% {
    background-position: -200% 0;
  }
}

@keyframes skeletonPulse {
  0%, 100% {
    opacity: 1;
  }
  50% {
    opacity: 0.8;
  }
}

@keyframes fadeInUp {
  0% {
    opacity: 0;
    transform: translateY(20px);
  }
  100% {
    opacity: 1;
    transform: translateY(0);
  }
}

/* Card Content Styles */
.card-image {
  position: relative;
  overflow: hidden;
  height: 200px;
  transform-style: preserve-3d;
}

.card-image img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: all 0.5s cubic-bezier(0.215, 0.61, 0.355, 1);
  transform: scale(1);
}

.card:hover .card-image img {
  transform: scale(1.15) rotate(0.5deg);
  filter: brightness(1.1) contrast(1.05);
}

.card-shine {
  position: absolute;
  top: 0;
  left: -100%;
  width: 50%;
  height: 100%;
  background: linear-gradient(
    90deg,
    transparent,
    rgba(255, 255, 255, 0.4),
    transparent
  );
  transition: left 0.6s ease;
  transform: skewX(-20deg);
}

.card:hover .card-shine {
  left: 150%;
}

.card-overlay {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: linear-gradient(
    135deg,
    rgba(102, 126, 234, 0.8) 0%,
    rgba(118, 75, 162, 0.8) 100%
  );
  display: flex;
  align-items: center;
  justify-content: center;
  opacity: 0;
  transition: all 0.4s cubic-bezier(0.215, 0.61, 0.355, 1);
  backdrop-filter: blur(2px);
}

.card:hover .card-overlay {
  opacity: 1;
  animation: overlayPulse 2s ease-in-out infinite;
}

@keyframes overlayPulse {
  0%, 100% {
    background: linear-gradient(
      135deg,
      rgba(102, 126, 234, 0.8) 0%,
      rgba(118, 75, 162, 0.8) 100%
    );
  }
  50% {
    background: linear-gradient(
      135deg,
      rgba(102, 126, 234, 0.9) 0%,
      rgba(118, 75, 162, 0.9) 100%
    );
  }
}

.view-btn {
  background: rgba(255, 255, 255, 0.95);
  border: none;
  padding: 0.75rem 1.5rem;
  border-radius: 25px;
  color: #333;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.3s ease;
  display: flex;
  align-items: center;
  gap: 0.5rem;
  font-size: 0.9rem;
  transform: translateY(20px);
  opacity: 0;
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.2);
}

.card:hover .view-btn {
  transform: translateY(0);
  opacity: 1;
  transition-delay: 0.1s;
}

.view-btn:hover {
  background: white;
  transform: scale(1.1) translateY(-2px);
  box-shadow: 0 6px 20px rgba(0, 0, 0, 0.3);
}

.card-body {
  padding: 1.5rem;
  position: relative;
  z-index: 2;
  background: white;
}

.card-title {
  font-size: 1.25rem;
  margin-bottom: 0.75rem;
  color: #333;
  font-weight: 600;
  line-height: 1.3;
  transition: color 0.3s ease;
}

.card:hover .card-title {
  color: #667eea;
}

.card-description {
  color: #666;
  font-size: 0.9rem;
  margin-bottom: 1.5rem;
  line-height: 1.5;
  display: -webkit-box;
  -webkit-line-clamp: 2;
  -webkit-box-orient: vertical;
  overflow: hidden;
  transition: color 0.3s ease;
}

.card:hover .card-description {
  color: #555;
}

.card-footer {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.project-info {
  display: flex;
  align-items: center;
  gap: 0.5rem;
}

.like-btn {
  background: none;
  border: 1px solid #ddd;
  padding: 0.5rem 1rem;
  border-radius: 20px;
  cursor: pointer;
  transition: all 0.3s cubic-bezier(0.175, 0.885, 0.32, 1.275);
  display: flex;
  align-items: center;
  gap: 0.5rem;
  font-size: 0.9rem;
  color: #666;
  position: relative;
  overflow: hidden;
}

.like-btn::before {
  content: '';
  position: absolute;
  top: 0;
  left: -100%;
  width: 100%;
  height: 100%;
  background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.4), transparent);
  transition: left 0.5s ease;
}

.like-btn:hover::before {
  left: 100%;
}

.like-btn:hover {
  border-color: #ff4757;
  color: #ff4757;
  transform: scale(1.05) translateY(-2px);
  box-shadow: 0 4px 12px rgba(255, 71, 87, 0.2);
}

.like-btn.liked {
  border-color: #ff4757;
  background: linear-gradient(135deg, rgba(255, 71, 87, 0.1) 0%, rgba(255, 71, 87, 0.05) 100%);
  color: #ff4757;
  animation: likePulse 0.6s ease;
}

@keyframes likePulse {
  0% {
    transform: scale(1);
  }
  50% {
    transform: scale(1.1);
  }
  100% {
    transform: scale(1);
  }
}

/* Error Message Styles */
.error-message {
  text-align: center;
  padding: 3rem 2rem;
  background: #fff5f5;
  border: 1px solid #fed7d7;
  border-radius: 16px;
  color: #c53030;
  margin: 2rem 0;
  animation: shake 0.5s ease-in-out;
}

@keyframes shake {
  0%, 100% { transform: translateX(0); }
  25% { transform: translateX(-5px); }
  75% { transform: translateX(5px); }
}

.error-message i {
  font-size: 3rem;
  margin-bottom: 1.5rem;
  color: #e53e3e;
  animation: bounce 2s infinite;
}

@keyframes bounce {
  0%, 20%, 50%, 80%, 100% {
    transform: translateY(0);
  }
  40% {
    transform: translateY(-10px);
  }
  60% {
    transform: translateY(-5px);
  }
}

.error-message p {
  margin-bottom: 1.5rem;
  font-size: 1.1rem;
}

.retry-btn {
  background: linear-gradient(135deg, #e53e3e 0%, #c53030 100%);
  color: white;
  border: none;
  padding: 0.75rem 1.5rem;
  border-radius: 8px;
  cursor: pointer;
  transition: all 0.3s ease;
  display: flex;
  align-items: center;
  gap: 0.5rem;
  margin: 0 auto;
  font-weight: 600;
  box-shadow: 0 4px 15px rgba(229, 62, 62, 0.3);
}

.retry-btn:hover {
  background: linear-gradient(135deg, #c53030 0%, #a53030 100%);
  transform: translateY(-2px);
  box-shadow: 0 6px 20px rgba(229, 62, 62, 0.4);
}

/* Loading Indicator */
.loading-indicator {
  text-align: center;
  padding: 2rem;
  color: #666;
  animation: fadeInUp 1s ease-out;
}

.spinner {
  width: 40px;
  height: 40px;
  border: 4px solid #e0e0e0;
  border-left: 4px solid #667eea;
  border-radius: 50%;
  animation: spin 1s linear infinite;
  margin: 0 auto 1rem;
}

@keyframes spin {
  0% { transform: rotate(0deg); }
  100% { transform: rotate(360deg); }
}

/* Responsive Design */
@media (max-width: 768px) {
  .cards-container {
    grid-template-columns: 1fr;
    gap: 1.5rem;
  }
  
  .section-title {
    font-size: 2rem;
  }
  
  .card-body {
    padding: 1.25rem;
  }
  
  .card-image {
    height: 180px;
  }
  
  .card:hover {
    transform: translateY(-8px) scale(1.01);
  }
}

@media (max-width: 480px) {
  .section-2 {
    padding: 2rem 0;
  }
  
  .section-title {
    font-size: 1.75rem;
  }
  
  .cards-container {
    gap: 1rem;
  }
}








/* Updated Chart Container Style */

.title-border {
  width: 120px;
  height: 4px;
  background: linear-gradient(90deg, #3498db, #9b59b6, #3498db);
  margin: 0 auto 30px;
  border-radius: 4px;
  animation: borderFlow 3s ease infinite;
}
.chart-wrapper {
  width: 100%;
  max-width: 1100px;
  margin: 0 auto;
  padding: 20px;
  border-radius: 12px;
  border: 1px solid #e3e3e3;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.08);
}

#chartDiv {
  width: 100%;
  height: 650px;
}

.title-section4{
  font-family: "Khmer OS Muol Light";
}

@media (max-width: 991px) {
  .section-4 {
    display: none !important;
  }
}


.progress-container {
  background-color: #e9ecef;
  border-radius: 5px;
  overflow: hidden;
  height: 8px;
}
.card-subtitle{
  text-align: left;
  font-weight: normal;
  font-size: 13px;
}
.progress-bar {
  background-color: orange;
  height: 8px;
  transition: width 0.3s ease;
}
.percentage {
  font-size: 12px;
  text-align: right;
  color: #333;
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
.social-icons i {
  transition: all 0.3s ease; /* Smooth animation */
  color: #ffffff; /* default color */
  cursor: pointer;
}

/* Hover effects with brand colors */
.social-icons i.bi-google:hover {
  color: #da4d40; /* Google Blue */
  transform: scale(1.2);
}

.social-icons i.bi-twitter-x:hover {
  color: black; /* Twitter X Blue */
  transform: scale(1.2);
}

.social-icons i.bi-facebook:hover {
  color: blue; /* Facebook Blue */
  transform: scale(1.2);
}

.social-icons i.bi-telegram:hover {
  color: #0088cc; /* Telegram Blue */
  transform: scale(1.2);
}

.social-icons i.bi-twitter:hover {
  color: #1DA1F2; /* Twitter Blue */
  transform: scale(1.2);
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
.title-section3{
  font-family: "Khmer OS Muol Light";
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
