<template>
  <nav class="navbar floating-navbar navbar-expand-lg sticky-top">
    <div class="container d-flex align-items-center justify-content-between">
      <!-- Navbar Logo -->
      <RouterLink class="navbar-brand fw-bold text-gradient" to="/">
        <i class="bi bi-lightning-charge-fill me-2"></i> Personal
      </RouterLink>

   

      <!-- Desktop Nav -->
      <div class="nav-links d-none d-lg-flex align-items-center">
        <RouterLink v-for="(link, i) in links" :key="i" :to="link.href" class="nav-link" :class="{ active: $route.path === link.href }">
          <i :class="link.icon"></i> 
          <span class="ms-1 nav-style">{{ link.name }}</span>
        </RouterLink>
      </div>

      <!-- Dark Mode Toggle -->
      <button class="darkmode-btn" @click="toggleDarkMode">
        <i :class="isDark ? 'bi bi-brightness-high-fill' : 'bi bi-moon-stars-fill'"></i>
      </button>

      <!-- Language on Navbar -->
      <div class="dropdown">
        <div class="box-flag dropdown-toggle" id="languageDropdown" data-bs-toggle="dropdown">
          <img :src="currentFlag" alt="flag" class="ms-3" style="width: 36px; height: 22px; object-fit: fill;" />
          {{ currentLanguage.value }}
        </div>

        <!-- Language Dropdown -->
        <ul class="dropdown-menu my-2" >
          <li v-for="lang in languages" :key="lang.code">
            <a class="dropdown-item d-flex align-items-center" href="#" @click.prevent="changeLanguage(lang.code)">
              <img :src="lang.flag" alt="flag" class="me-3 my-2" style="width: 32px; height: 22px; object-fit: cover;">
              {{ lang.name }}
            </a>
          </li>
        </ul>
      </div>

      <!-- Button Collape Sidebar -->
      <div class="d-flex align-items-center">
        <!-- Button Toggler for (Mobile) -->
        <button v-if="!sidebarOpen" class="custom-toggler" type="button" @click="toggleSidebar">
          <span :class="{ 'open-span-1': sidebarOpen }"></span>
          <span :class="{ 'open-span-2': sidebarOpen }"></span>
          <span :class="{ 'open-span-3': sidebarOpen }"></span>
        </button>
      </div>
    </div>

    <!-- Mobile Sidebar -->
    <transition name="slide">
      <div class="mobile-sidebar d-lg-none" v-show="sidebarOpen">
        <button class="close-btn" @click="closeSidebar">✕</button>

        <ul class="nav flex-column mt-5">
          <li v-for="(link, i) in links" :key="i" class="nav-item my-3">
            <RouterLink class="sidebar-link d-flex align-items-center justify-content-start p-2 rounded-3"
              :to="link.href" @click="closeSidebar">
              <i :class="link.icon" class="me-3 fs-4"></i>
              <span class="fw-semibold fs-5">{{ link.name }}</span>
            </RouterLink>
          </li>
        </ul>

        <!-- Bottom Version -->
        <div class="sidebar-footer mt-auto text-center p-3">
          <span>Version 0.0.1</span>
        </div>
      </div>
    </transition>

    <!-- Overlay Opacity Background -->
    <transition name="fade">
      <div v-if="sidebarOpen" class="overlay" @click="closeSidebar"></div>
    </transition>
  </nav>
</template>

<script setup>
import { ref, watch, computed,  onUnmounted, onMounted } from "vue";
import { RouterLink } from "vue-router";
import { currentLanguage } from "../stores/languageStore.js";

const sidebarOpen = ref(false);
const isDark = ref(false);
const languages = [
  { code: "EN", name: "English", flag: "./flags/flag_english.png" },
  { code: "KH", name: "ខ្មែរ", flag: "./flags/flag_cambodia.png" }
];

// Computed property to get the current flag
const currentFlag = computed(() => {
  const lang = languages.find(l => l.code === currentLanguage.value);
  return lang ? lang.flag : "";
});

const changeLanguage = (code) => {
  currentLanguage.value = code;

  const btn = document.getElementById("languageDropdown");
  if (btn) {
    btn.classList.add("animate-language");
    setTimeout(() => btn.classList.remove("animate-language"), 500);
  }
};

const links = computed(() => linkTranslations[currentLanguage.value]);
const linkTranslations = {
  EN: [
    { name: "Home", href: "/", icon: "bi bi-house-door" },
    { name: "About", href: "/about", icon: "bi bi-person" },
    { name: "Experience", href: "/experience", icon: "bi bi-briefcase" },
    { name: "Contact", href: "/Contact", icon: "bi bi-phone" }
  ],

  KH: [
    { name: "ទំព័រដើម", href: "/", icon: "bi bi-house-door" },
    { name: "អំពីយើងខ្ញុំ", href: "/about", icon: "bi bi-person" },
    { name: "បទពិសោធន៍", href: "/experience", icon: "bi bi-briefcase" },
    { name: "ទំនាក់ទំនង", href: "/Contact", icon: "bi bi-phone" }
  ]
};
const toggleSidebar = () => (sidebarOpen.value = !sidebarOpen.value);
const closeSidebar = () => (sidebarOpen.value = false);

// Toggle Dark Mode
const toggleDarkMode = () => {
  isDark.value = !isDark.value;
  document.documentElement.setAttribute("data-theme", isDark.value ? "dark" : "light");
  localStorage.setItem("theme", isDark.value ? "dark" : "light");
};


watch(sidebarOpen, (isOpen) => {
  document.body.style.overflow = isOpen ? "hidden" : "";
});

onUnmounted(() => {
  document.body.style.overflow = "";
});

// 👇 Auto-close sidebar on window resize
const handleResize = () => {
  if (window.innerWidth >= 992 && sidebarOpen.value) {
    sidebarOpen.value = false;
  }
};

onMounted(() => {
  window.addEventListener("resize", () => {
    document.body.classList.add("no-transition");
    if (window.innerWidth >= 992 && sidebarOpen.value) {
      sidebarOpen.value = false;
    }
    // remove the class after a short delay
    setTimeout(() => document.body.classList.remove("no-transition"), 200);
  });
});

onUnmounted(() => {
  window.removeEventListener("resize", handleResize);
});
</script>

<style scoped>
/* 🌟 NAVBAR */
.floating-navbar {
  /* background: rgba(255, 255, 255, 0.9); */
  backdrop-filter: blur(12px);
  border-radius: 14px;
  padding: 0.9rem 1.5rem;
  margin: 1rem auto;
  max-width: 1200px;
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.08);
  transition: all 0.4s ease;
  z-index: 1000;
}
/* 🌗 DARK MODE BUTTON */
:root[data-theme="light"] {
  --bg-gradient: radial-gradient(circle, #da4d40 0%, #7a2828 100%);
  --text-color: white;
}
:root[data-theme="dark"] {
  --bg-gradient: radial-gradient(circle, #2c313c 0%, 	#343b48 100%);
  --text-color: #f5f5f5;
}
nav.navbar {
  background-color: var(--bg-gradient);
  color: var(--text-color);
  transition: background-color 0.3s, color 0.3s;
  font-family: "Khmer OS Metal Chrieng";
}

.darkmode-btn {
  margin-left: 10%;
  border: none;
  background: transparent;
  font-size: 1.4rem;
  color: white;
  cursor: pointer;
  transition: color 0.5s ease, transform 0.3s;

}
.darkmode-btn i {
  font-size: 1.4rem;
  cursor: pointer;
}
.darkmode-btn:hover {
  color: #ff7e5f;
  transform: rotate(30deg);
}
/* Smooth language switch animation */
.box-flag {
  display: inline-block;
  transition: transform 0.3s ease;
}

.box-flag:hover {
  cursor: pointer;
  transform: translateY(0px) scale(1.1);
}
.dropdown-item{
  font-family: "Khmer OS Battambang";
}
.animate-language {
  animation: bounce 0.5s ease;
}

@keyframes bounce {
  0% { transform: scale(1); }
  25% { transform: scale(1.2); }
  50% { transform: scale(0.9); }
  75% { transform: scale(1.1); }
  100% { transform: scale(1); }
}

.navbar-brand{
  transition: all 0.3s ease;
}

.text-gradient {
  background: linear-gradient(60deg, #ff7e5f, #feb47b);
  -webkit-background-clip: text;
  color: white;
  font-size: 1.6rem;
}

/* NAV LINKS */
.nav-link {
  color: white !important;
  font-weight: 500;
  font-size: 1.1rem;
  margin-left: 1.5rem;
  padding: 0.35rem 0.6rem;
  position: relative; /* needed for pseudo-element */
  transition: transform 0.3s ease;
}

.nav-link::after {
  content: '';
  position: absolute;
  left: 0;
  bottom: 0;
  width: 0;
  height: 2px;
  background-color: #feb47b;
  transition: width 0.5s ease;
}
.nav-link:hover::after {
  width: 100%;
}
/* Active link style */
.nav-link.active {
  color: #feb47b !important; /* optional: change text color */
}

.nav-link.active::after {
  width: 100%; /* underline stays visible on active link */
}


/* HAMBURGER */
.custom-toggler {
  border: none;
  background: transparent;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  width: 32px;
  height: 24px;
  cursor: pointer;
  z-index: 1101;
}
.custom-toggler span {
  display: block;
  height: 3px;
  width: 100%;
  background: white;
  border-radius: 3px;
  transition: all 0.35s ease;
}
.open-span-1 {
  transform: rotate(45deg) translate(6px, 6px);
  background: #ff7e5f;
}
.open-span-2 {
  opacity: 0;
}
.open-span-3 {
  transform: rotate(-45deg) translate(6px, -6px);
  background: #ff7e5f;
}

/* MOBILE SIDEBAR */
.mobile-sidebar {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  position: fixed;
  top: 0;
  right: 0;
  width: 260px;
  height: 100vh;
  background: rgba(255, 255, 255, 0.97);
  backdrop-filter: blur(10px);
  box-shadow: -8px 0 25px rgba(0, 0, 0, 0.15);
  padding: 2rem 1.5rem;
  z-index: 2100;
  border-top-left-radius: 20px;
  border-bottom-left-radius: 20px;


}
.mobile-sidebar .nav-link {
  color: #444 !important;
  font-size: 1.3rem;
  transition: all 0.3s ease;
}
.mobile-sidebar .nav-link:hover {
  color: #ff7e5f !important;
  transform: scale(1.05);
}

/* CLOSE BUTTON */
.close-btn {
  position: absolute;
  top: 15px;
  left: 15px;
  background: none;
  border: none;
  color: #444;
  font-size: 1.9rem;
  cursor: pointer;
  transition: color 0.3s;
  z-index: 1110;
}
.close-btn:hover {
  color: #ff7e5f;
}

/* OVERLAY */
.overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100vh;
  background: rgba(0, 0, 0, 0.25);
  backdrop-filter: blur(2px);
  z-index: 1090;
}
.sidebar-footer {
  border-top: 1px solid gainsboro;
  font-size: 0.9rem;
  color: gray;
  text-align: center;
  padding-top: 0.75rem;
}

/* ANIMATIONS */
.sidebar-link {
  color: #444;
  background: rgba(255, 255, 255, 0.2);
  transition: all 0.3s ease;
  text-decoration: none;
}
.sidebar-link:hover {
  color: #ff7e5f;
  background: rgba(255, 126, 95, 0.1);
  transform: translateX(2px);
  box-shadow: 0 2px 8px rgba(230, 229, 229, 0.2);
}
.sidebar-link i {
  min-width: 32px; /* keep icons aligned */
  text-align: center;
}
.slide-enter-active,
.slide-leave-active {
  transition: all 0.35s ease;
}
.slide-enter-from,
.slide-leave-to {
  transform: translateX(100%);
}
.no-transition .slide-enter-active,
.no-transition .slide-leave-active {
  transition: all 0s ease !important;
}
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.1s ease;
}
.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}

/* RESPONSIVE */
@media (max-width: 991px) {
  .floating-navbar {
    border-radius: 0;
    margin: 0;
    max-width: 100%;
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
  }
    .dropdown-menu {
    margin-left: -70%;
  }
  .darkmode-btn {
    margin-left: 20%;
  }
}
@media (min-width: 992px) {
  .custom-toggler {
    
  }
}
/* 📱 Fix layout when screen < 440px */
@media (max-width: 440px) {

  .floating-navbar {
    padding: 0.5rem 0.8rem;
  }

  /* shrink logo */
  .navbar-brand {
    font-size: 1.2rem;
  }

  /* Reduce darkmode button size */
  .darkmode-btn {
    margin-left: 5%;
    font-size: 1.1rem;
  }
  .darkmode-btn i {
    font-size: 1.1rem;
  }

  /* Make language selector smaller */
  .box-flag {
    font-size: 0.8rem;
  }
  .box-flag img {
    width: 28px !important;
    height: 18px !important;
  }

  /* Fix dropdown position so it does NOT overflow the screen */
  .dropdown-menu {
    left: -50px !important;
    transform: translateX(-30%);
  }

  /* Shrink hamburger button */
  .custom-toggler {
    width: 28px;
    height: 20px;
  }
  .custom-toggler span {
    height: 2px;
  }
}

</style>
