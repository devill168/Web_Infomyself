<template>
  <nav class="navbar floating-navbar navbar-expand-lg sticky-top">
    <div class="container d-flex align-items-center justify-content-between">
      <!-- Brand -->
      <RouterLink class="navbar-brand fw-bold text-gradient" to="/">
        <i class="bi bi-lightning-charge-fill me-2"></i> Personal
      </RouterLink>

      <!-- Button Toggler for (Mobile) -->
      <button v-if="!sidebarOpen" class="custom-toggler" type="button" @click="toggleSidebar">
        <span :class="{ 'open-span-1': sidebarOpen }"></span>
        <span :class="{ 'open-span-2': sidebarOpen }"></span>
        <span :class="{ 'open-span-3': sidebarOpen }"></span>
      </button>

      <!-- Desktop Nav -->
      <div class="nav-links d-none d-lg-flex align-items-center">
        <RouterLink v-for="(link, i) in links" :key="i" class="nav-link" :to="link.href">
          <i :class="link.icon"></i>
          <span class="ms-1">{{ link.name }}</span>
        </RouterLink>
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
import { ref, watch, onUnmounted, onMounted } from "vue";
import { RouterLink } from "vue-router";

const sidebarOpen = ref(false);

const links = [
  { name: "Home", href: "/", icon: "bi bi-house-door" },
  { name: "About", href: "/about", icon: "bi bi-person" },
  { name: "Experience", href: "/experience", icon: "bi bi-briefcase" },
  { name: "Contact", href: "/Contact", icon: "bi bi-phone" },
];

const toggleSidebar = () => (sidebarOpen.value = !sidebarOpen.value);
const closeSidebar = () => (sidebarOpen.value = false);

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
  window.addEventListener("resize", handleResize);
});

onUnmounted(() => {
  window.removeEventListener("resize", handleResize);
});
</script>

<style scoped>
/* 🌟 NAVBAR */
.floating-navbar {
  background: rgba(255, 255, 255, 0.9);
  backdrop-filter: blur(12px);
  border-radius: 14px;
  padding: 0.9rem 1.5rem;
  margin: 1rem auto;
  max-width: 1200px;
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.08);
  transition: all 0.4s ease;
  z-index: 1000;
}

.text-gradient {
  background: linear-gradient(60deg, #ff7e5f, #feb47b);
  -webkit-background-clip: text;
  color: transparent;
  font-size: 1.6rem;
}

/* NAV LINKS */
.nav-link {
  color: #444 !important;
  font-weight: 500;
  font-size: 1.1rem;
  margin-left: 1.5rem;
  padding: 0.35rem 0.6rem;
  border-radius: 8px;
  transition: all 0.3s ease;
}
.nav-link:hover {
  color: #ff7e5f !important;
  background: rgba(255, 126, 95, 0.1);
  transform: translateY(-2px);
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
  background: #444;
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
}
@media (min-width: 992px) {
  .custom-toggler {
    display: none;
  }
}
</style>
