<template>
  <div class="container py-5">
    <!-- Section 1 -->
    <section class="intro-section py-5">
      <div class="text-center">
        <h1>{{ section1.title }}</h1>
        <div class="border-line"></div>
        <p>{{ section1.description }}</p>
      </div>
    </section>

    <!-- Section 2 -->
    <section class="experience-section">
      <h1 class="text-center">{{ section2.title }}</h1>
      
      <!-- Enhanced Todo List / Timeline -->
      <div class="todo-container">
        <div 
          v-for="(experience, index) in experiences" 
          :key="index"
          class="todo-item"
          :class="{ 
            'active': isVisible[index],
            'hovered': hoverIndex === index,
            'completed': index < currentExpIndex
          }"
          @mouseenter="hoverIndex = index"
          @mouseleave="hoverIndex = -1"
          @click="setCurrentExp(index)"
        >
          <!-- Progress Line -->
          <div class="progress-line" v-if="index < experiences.length - 1"></div>
          
          <!-- Todo Checkbox -->
          <div class="todo-checkbox">
            <div class="checkbox-circle">
              <div class="check-icon">
                <svg width="14" height="14" viewBox="0 0 24 24" fill="none">
                  <path d="M20 6L9 17L4 12" stroke="currentColor" stroke-width="3" stroke-linecap="round" stroke-linejoin="round"/>
                </svg>
              </div>
            </div>
          </div>

          <!-- Todo Content -->
          <div class="todo-content">
            <div class="todo-header">
              <h3 class="position">
                <span class="position-icon">
                  <svg width="20" height="20" viewBox="0 0 24 24" fill="none">
                    <path d="M21 16V8.00002C20.9996 7.6493 20.9071 7.30483 20.7315 7.00119C20.556 6.69754 20.3037 6.44539 20 6.27002L13 2.27002C12.696 2.09449 12.3511 2.00208 12 2.00208C11.6489 2.00208 11.304 2.09449 11 2.27002L4 6.27002C3.69626 6.44539 3.44398 6.69754 3.26846 7.00119C3.09294 7.30483 3.00036 7.6493 3 8.00002V16C3.00036 16.3508 3.09294 16.6952 3.26846 16.9989C3.44398 17.3025 3.69626 17.5547 4 17.73L11 21.73C11.304 21.9056 11.6489 21.998 12 21.998C12.3511 21.998 12.696 21.9056 13 21.73L20 17.73C20.3037 17.5547 20.556 17.3025 20.7315 16.9989C20.9071 16.6952 20.9996 16.3508 21 16Z" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
                    <path d="M3.27002 6.96002L12 12L20.73 6.96002" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
                    <path d="M12 22.08V12" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
                  </svg>
                </span>
                {{ experience.position }}
              </h3>
              <span class="duration-badge">
                <span class="calendar-icon">
                  <svg width="14" height="14" viewBox="0 0 24 24" fill="none">
                    <rect x="3" y="4" width="18" height="18" rx="2" ry="2" stroke="currentColor" stroke-width="2"/>
                    <line x1="16" y1="2" x2="16" y2="6" stroke="currentColor" stroke-width="2"/>
                    <line x1="8" y1="2" x2="8" y2="6" stroke="currentColor" stroke-width="2"/>
                    <line x1="3" y1="10" x2="21" y2="10" stroke="currentColor" stroke-width="2"/>
                  </svg>
                </span>
                {{ experience.duration }}
              </span>
            </div>
            
            <p class="company">
              <span class="company-icon">
                <svg width="16" height="16" viewBox="0 0 24 24" fill="none">
                  <path d="M19 21V5C19 3.89543 18.1046 3 17 3H7C5.89543 3 5 3.89543 5 5V21M19 21L21 21M19 21H14M5 21L3 21M5 21H10M9 6.99998H15M9 11H15M9 15H15" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
                </svg>
              </span>
              {{ experience.company }}
            </p>

            <div class="description-container" :class="{ 'expanded': expandedIndex === index }">
              <p class="description">{{ experience.description }}</p>
              <button 
                v-if="experience.description.length > 150"
                class="read-more-btn"
                @click.stop="toggleDescription(index)"
              >
                {{ expandedIndex === index ? 
                  (currentLanguage === 'KH' ? 'បង្រួម' : 'Read Less') : 
                  (currentLanguage === 'KH' ? 'អានបន្ថែម' : 'Read More') 
                }}
              </button>
            </div>

            <div class="skills">
              <span 
                v-for="(skill, skillIndex) in experience.skills" 
                :key="skillIndex"
                class="skill-tag"
                :style="{ 
                  'animation-delay': `${skillIndex * 0.1}s`,
                  '--tag-index': skillIndex 
                }"
              >
                <span class="skill-icon">
                  <svg width="12" height="12" viewBox="0 0 24 24" fill="none">
                    <path d="M20 6L9 17L4 12" stroke="currentColor" stroke-width="3" stroke-linecap="round" stroke-linejoin="round"/>
                  </svg>
                </span>
                {{ skill }}
              </span>
            </div>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>

<script setup>
import { ref, computed, onMounted, onUnmounted } from "vue";
import { currentLanguage } from "../stores/languageStore.js";

// Animation and interaction states
const isVisible = ref([]);
const hoverIndex = ref(-1);
const currentExpIndex = ref(0);
const expandedIndex = ref(-1);

// Content based on language
const section1 = computed(() => {
  return currentLanguage.value === "KH" 
    ? {
        title: "បទពិសោធន៍ការងារ",
        description: "ពេលវេលានៃវឌ្ឍនភាពអាជីពរបស់ខ្ញុំ ការអភិវឌ្ឍន៍ជំនាញ និងសមិទ្ធផលសំខាន់ៗក្នុងពេលបច្ចុប្បន្ន"
      }
    : {
        title: "Work Experience",
        description: "A timeline of my career progression, skills development, and key achievements"
      };
});

const section2 = computed(() => {
  return currentLanguage.value === "KH" 
    ? "បទពិសោធន៍ការងារ"
    : "Work Experience";
});

// Experience data
const experiences = computed(() => {
  return currentLanguage.value === "KH"
    ? [
        {
          position: "បុគ្គលិកស្ម័គ្រចិត្ត បញ្ចូលទិន្នន័យ",
          company: "ក្រុមហ៊ុន យូរស្មាត",
          duration: "2013 - 2015",
          description: "ប្រមូលទិន្នន័យ ផ្ទៀងផ្ទាត់ទិន្នន័យស្តុកទំនិញ និង បញ្ចូលទិន្នន័យចូលកម្មវិធីគ្រប់គ្រងឃ្លាំង",
          skills: ["ប្រមូលទិន្នន័យ", "បញ្ចូលទិន្នន័យ", "វិភាគទិន្នន័យ"]
        },
        {
          position: "មន្រ្តីកិច្ចសន្យាព័ត៌មានវិទ្យា",
          company: "មន្រ្តីកិច្ចសន្យាព័ត៌មានវិទ្យានៃមជ្ឈមណ្ឌលជាតិប្រយុទ្ធនឹងជំងឺគ្រុនចាញ់ ប៉ារ៉ាស៊ីតសាស្ត្រ និងបាណកសាស្ត្រ ក្រសួងសុខាភិបាល",
          duration: "2015 - 2019",
          description: "ជួសជុលកុំព្យូទ័រ តភ្ជាប់បណ្តាញ Netwrok នៅក្នុងអង្គភាព និង ជួយសម្របសម្រួលការងារផ្សេងៗពាក់ព័ន្ធព័ត៌មានវិទ្យា",
          skills: ["ថែទាំកុំព្យូទ័រតាមផ្នែក", "បណ្តាញ", "CISCO"]
        },
        {
          position: "មន្រ្តីស្ម័គ្រចិត្តភូមិព្យាបាលជំងឺគ្រុនចាញ់ ",
          company: "មន្រ្តីស្ម័គ្រចិត្តភូមិព្យាបាលជំងឺគ្រុនចាញ់នៃមជ្ឈមណ្ឌលជាតិប្រយុទ្ធនឹងជំងឺគ្រុនចាញ់ ប៉ារ៉ាស៊ីតសាស្ត្រ និងបាណកសាស្ត្រ ក្រសួងសុខាភិបាល",
          duration: "2019 - 2021",
          description: "ជួយសម្របសម្រួលការងារជាមួយថ្នាក់ខេត្ត រៀបចំផែនការណ៍សកម្មភាពបេសកកម្ម, រៀបចំផែនការណ៍កញ្ចប់ថវិកាសម្រាប់ផ្នែក, រៀបចំផែនការលទ្ធកម្ម, រៀបចំផែនការណ៍សកម្មភាពលើវគ្គបណ្តុះបណ្តាលផ្សេងៗលើអង្គភាព",
          skills: ["គ្រប់គ្រង/វិភាគទិន្នន័យ", "សម្របសម្រួល", "លទ្ធកម្ម, រៀបចំផែនការ"]
        },
        {
          position: "មន្ត្រីផ្នែកអភិវឌ្ឈន៍ប្រព័ន្ធទិន្នន័យ",
          company: "មន្ត្រីព័ត៌មានវិទ្យានៃមជ្ឈមណ្ឌលជាតិប្រយុទ្ធនឹងជំងឺគ្រុនចាញ់ ប៉ារ៉ាស៊ីតសាស្ត្រ និងបាណកសាស្ត្រ ក្រសួងសុខាភិបាល",
          duration: "2022 - បច្ចុប្បន្ន",
          description: "បង្កើតកម្មវិធីបញ្ចូលទិន្នន័យដូចជា Google Sheet, Epidata, EpiInfo, Front-End Web Design",
          skills: ["Tool Desgin PS AI AE", "HTML/CSS/Boostrap/Knockout.JS", "Adobe XD, Figma"]
        }
      ]
    : [
        {
          position: "Data Entry Officer",
          company: "Usmart Company.",
          duration: "2019 - Present",
          description: "Collect warehouse data and data entry on Inventory management system",
          skills: ["Data Collection", "Data Entry", "Data Analyzer"]
        },
        {
          position: "IT Officer",
          company: "IT Officer at National center parasitology entomology and malaria control Ministry of Health",
          duration: "2015 - 2019",
          description: "Repair computers, connect to the network in the organization, and help coordinate other IT-related tasks.",
          skills: ["Office Support", "Network", "CISCO"]
        },
            {
          position: "VMW Officer",
          company: "Village Malaria Worker Officer at Department of drugs and food Ministry of Health.",
          duration: "2019 - 2021",
          description: "Provide technical assistance in information technology to staff, officers, and leaders, and provide technical assistance in systems, inspecting and monitoring the management of medicines and medical equipment, and teaching how to use all systems, ensuring system stability, and managing information technology assets.",
          skills: ["Data Management", "Coordination", "Procument, Develop an action plan"]
        },
        {
          position: "Developer Officer",
          company: "Developer Officer at National center parasitology entomology and malaria control Ministry of Health.",
          duration: "2022 - Present",
          description: "Create form in system such as Google Sheet, Epidata, EpiInfo, Front-End Web Design.",
          skills: ["Tool Desgin PS AI AE", "HTML/CSS/Boostrap/Knockout.JS", "Adobe XD, Figma"]
        }
      ];
});

// Interaction functions
const setCurrentExp = (index) => {
  currentExpIndex.value = index;
};

const toggleDescription = (index) => {
  expandedIndex.value = expandedIndex.value === index ? -1 : index;
};

// Intersection Observer for scroll animations
let observer;

onMounted(() => {
  // Initialize visibility array
  isVisible.value = new Array(experiences.value.length).fill(false);
  
  // Set up intersection observer for scroll animations
  observer = new IntersectionObserver((entries) => {
    entries.forEach(entry => {
      if (entry.isIntersecting) {
        const index = parseInt(entry.target.dataset.index);
        setTimeout(() => {
          isVisible.value[index] = true;
        }, index * 300); // Stagger animation
      }
    });
  }, { threshold: 0.15 });
  
  // Observe all todo items
  document.querySelectorAll('.todo-item').forEach((item, index) => {
    item.dataset.index = index;
    observer.observe(item);
  });
});

onUnmounted(() => {
  if (observer) {
    observer.disconnect();
  }
});
</script>

<style scoped>
.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 20px;
}

/* Section 1 */
.intro-section {
  margin-bottom: 4rem;
  text-align: center;
}

  .intro-section h1 {
    line-height: 80px;
    font-size: 2.5rem;
    margin-bottom: 1rem;
    background: linear-gradient(135deg, white, #d1d1d1, #2c3e50);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
    font-family: "Khmer OS Muol Light";
  }

.border-line {
  width: 80px;
  height: 4px;
  background: linear-gradient(to right, #3498db, #2c3e50);
  margin: 0 auto 1.5rem;
  border-radius: 2px;
  position: relative;
  overflow: hidden;
}

.border-line::after {
  content: '';
  position: absolute;
  top: 0;
  left: -100%;
  width: 100%;
  height: 100%;
  background: linear-gradient(90deg, transparent, rgba(255,255,255,0.6), transparent);
  animation: shimmer 2s infinite;
}

@keyframes shimmer {
  0% { left: -100%; }
  100% { left: 100%; }
}

.intro-section p {
  font-size: 1.2rem;
  color: #d1d1d1;
  max-width: 700px;
  margin: 0 auto;
  line-height: 1.6;
}

/* Section 2 */
.experience-section h1 {
  font-size: 2.2rem;
  margin-bottom: 3rem;
  color: #2c3e50;
  background: linear-gradient(135deg, #2c3e50, #3498db);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

/* Enhanced Todo Container */
.todo-container {
  position: relative;
  max-width: 900px;
  margin: 0 auto;
  padding: 2rem 0;
}

.todo-item {
  position: relative;
  display: flex;
  align-items: flex-start;
  gap: 1.5rem;
  margin-bottom: 3rem;
  padding: 2rem;
  background: white;
  border-radius: 16px;
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.08);
  border: 2px solid transparent;
  transition: all 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275);
  opacity: 0;
  transform: translateX(-50px) scale(0.95);
  cursor: pointer;
}

.todo-item.active {
  opacity: 1;
  transform: translateX(0) scale(1);
  animation: slideIn 0.6s cubic-bezier(0.175, 0.885, 0.32, 1.275) forwards;
}

.todo-item.hovered {
  border-color: #3498db;
  box-shadow: 0 8px 30px rgba(52, 152, 219, 0.2);
  transform: translateY(-5px) scale(1.02);
}

.todo-item.completed {
  background: linear-gradient(135deg, #f8f9ff 0%, #ffffff 100%);
}

@keyframes slideIn {
  0% {
    opacity: 0;
    transform: translateX(-50px) scale(0.95);
  }
  100% {
    opacity: 1;
    transform: translateX(0) scale(1);
  }
}

/* Progress Line */
.progress-line {
  position: absolute;
  left: 2.5rem;
  top: 4.5rem;
  bottom: -3.5rem;
  width: 2px;
  background: linear-gradient(to bottom, #3498db, #e0e0e0);
  z-index: 1;
}

.todo-item:last-child .progress-line {
  display: none;
}

/* Todo Checkbox */
.todo-checkbox {
  position: relative;
  z-index: 2;
  flex-shrink: 0;
}

.checkbox-circle {
  width: 3rem;
  height: 3rem;
  border-radius: 50%;
  background: linear-gradient(135deg, #3498db, #2c3e50);
  display: flex;
  align-items: center;
  justify-content: center;
  box-shadow: 0 4px 15px rgba(52, 152, 219, 0.3);
  transition: all 0.3s ease;
  position: relative;
  overflow: hidden;
}

.checkbox-circle::before {
  content: '';
  position: absolute;
  top: 0;
  left: -100%;
  width: 100%;
  height: 100%;
  background: linear-gradient(90deg, transparent, rgba(255,255,255,0.4), transparent);
  transition: left 0.5s ease;
}

.todo-item.hovered .checkbox-circle::before {
  left: 100%;
}

.check-icon {
  color: white;
  opacity: 0;
  transform: scale(0.5);
  transition: all 0.3s ease;
}

.todo-item.completed .check-icon {
  opacity: 1;
  transform: scale(1);
}

/* Todo Content */
.todo-content {
  flex: 1;
  min-width: 0;
}

.todo-header {
  display: flex;
  justify-content: between;
  align-items: flex-start;
  margin-bottom: 1rem;
  gap: 1rem;
  font-family: "Khmer OS Muol Light";
}

.position {
  margin: 0;
  color: #2c3e50;
  font-size: 1.4rem;
  font-weight: 700;
  flex: 1;
  display: flex;
  align-items: center;
  gap: 0.5rem;
}

.position-icon {
  color: #3498db;
  opacity: 0.8;
}

.duration-badge {
  background: linear-gradient(135deg, #3498db, #2c3e50);
  color: white;
  padding: 0.5rem 1rem;
  border-radius: 20px;
  font-size: 0.85rem;
  font-weight: 600;
  display: flex;
  align-items: center;
  gap: 0.5rem;
  white-space: nowrap;
}

.calendar-icon {
  opacity: 0.9;
}

.company {
  color: #7f8c8d;
  font-weight: 600;
  margin-bottom: 1rem;
  display: flex;
  align-items: center;
  gap: 0.5rem;
  font-family: "Khmer OS Muol Light";
  line-height: 30px;
}

.company-icon {
  color: #3498db;
  opacity: 0.7;
}

/* Description */
.description-container {
  position: relative;
  margin-bottom: 1.5rem;
}

.description {
  color: #555;
  line-height: 1.7;
  margin-bottom: 1rem;
  transition: all 0.3s ease;
  font-family: "Khmer OS Battambang";
}

.description-container:not(.expanded) .description {
  display: -webkit-box;
  -webkit-line-clamp: 3;
  -webkit-box-orient: vertical;
  overflow: hidden;
}

.read-more-btn {
  background: none;
  border: none;
  color: #3498db;
  font-weight: 600;
  cursor: pointer;
  padding: 0.25rem 0;
  font-size: 0.9rem;
  transition: all 0.3s ease;
}

.read-more-btn:hover {
  color: #2980b9;
  transform: translateX(5px);
}

/* Skills */
.skills {
  display: flex;
  flex-wrap: wrap;
  gap: 0.75rem;
  font-family: "Khmer OS Battambang";
}

.skill-tag {
  background: linear-gradient(135deg, #e3f2fd, #bbdefb);
  color: #1565c0;
  padding: 0.5rem 1rem;
  border-radius: 25px;
  font-size: 0.75rem;
  font-weight: 600;
  display: flex;
  align-items: center;
  gap: 0.5rem;
  transition: all 0.3s ease;
  animation: tagPopIn 0.5s ease forwards;
  animation-delay: calc(var(--tag-index) * 0.1s);
  opacity: 0;
  transform: translateY(10px);
}

@keyframes tagPopIn {
  0% {
    opacity: 0;
    transform: translateY(10px) scale(0.8);
  }
  100% {
    opacity: 1;
    transform: translateY(0) scale(1);
  }
}

.todo-item.active .skill-tag {
  animation: tagPopIn 0.5s ease forwards;
}

.todo-item.hovered .skill-tag {
  background: linear-gradient(135deg, #1565c0, #1976d2);
  color: white;
  transform: translateY(-2px) scale(1.05);
  box-shadow: 0 4px 12px rgba(21, 101, 192, 0.3);
}

.skill-icon {
  opacity: 0.8;
}

/* Responsive Design */
@media (max-width: 991px) {
  .experience-section {
    margin-top: 10%;
  }
  
  .todo-item {
    padding: 1.5rem;
    gap: 1rem;
  }
  
  .checkbox-circle {
    width: 2.5rem;
    height: 2.5rem;
  }
  
  .progress-line {
    left: 2.25rem;
  }
  
  .intro-section h1,
  .experience-section h1 {
    font-size: 2rem;
  }
}

@media (max-width: 768px) {
  .intro-section h1,
  .experience-section h1 {
    font-size: 1.8rem;
  }
  
  .todo-item {
    flex-direction: column;
    padding: 1.5rem;
    gap: 1rem;
  }
  
  .todo-header {
    flex-direction: column;
    align-items: flex-start;
    gap: 0.75rem;
  }
  
  .progress-line {
    display: none;
  }
  
  .position {
    font-size: 1.2rem;
  }
}

.text-center {
  text-align: center;
}
</style>