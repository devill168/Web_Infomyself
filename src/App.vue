<template>
<div id="app" class="app-container">
    <Navbar @toggle-dark="toggleDarkMode" />
    <RouterView />
    <FooterVue />
  </div>
</template>

<script setup>
import { ref} from "vue";
import Navbar from "./components/Navbar.vue";
import FooterVue from "./components/Footer.vue";


const isDark = ref(false); // always light mode on refresh
document.documentElement.setAttribute("data-theme", "light");

const toggleDarkMode = () => {
  isDark.value = !isDark.value;
  document.documentElement.setAttribute("data-theme", isDark.value ? "dark" : "light");
  // optional: remove localStorage saving
  localStorage.removeItem("theme");
};
</script>


<style>
/* Global Theme Variables */
:root[data-theme="light"] {
  --bg-gradient: radial-gradient(circle, #da4d40 0%, #7a2828 100%);
  --text-color: white;
}
:root[data-theme="dark"] {
  --bg-gradient: radial-gradient(circle, #3c4454 0%, 	#2c313c 100%);
  --text-color: white;
}
body,
html,
.app-container {
  background: var(--bg-gradient);
  color: var(--text-color);
  transition: background 0.5s ease, color 0.5s ease;
  min-height: 100vh;
  margin: 0;
}

/* ✅ Wrapper fills full viewport */
/* .app-wrapper {
  min-height: 100vh;
  width: 100%;
  background: radial-gradient(circle, #da4d40 0%, #7a2828 100%);
  transition: background 0.6s ease;
  overflow-x: hidden;
} */

/* ✅ Dark mode full background */
/* .app-wrapper.dark {
  background: #000;
  color: #fff;
} */

/* Make sure Navbar stays visible above everything */
/* nav.navbar {
  z-index: 1000;
} */
</style>
