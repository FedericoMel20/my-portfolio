<template>
  <header class="topbar">
    
    <!-- LEFT SIDE: FLAG + MB -->
    <div class="brand">
      <div class="flag-circle">
        <img src="/gambia-flag.png" alt="Gambian Flag" />
      </div>
      <span class="brand-text">MB</span>
    </div>

    <!-- NAVIGATION -->
    <nav class="nav">
      <router-link 
        to="/" 
        class="nav-item" 
        :class="{ active: isActive('/') }">
        HOME
      </router-link>

      <router-link 
        to="/profile" 
        class="nav-item" 
        :class="{ active: isActive('/profile') }">
        PROFILE
      </router-link>

      <router-link 
        to="/portfolio" 
        class="nav-item" 
        :class="{ active: isActive('/portfolio') }">
        PORTFOLIO
      </router-link>
    </nav>

    <!-- RIGHT SIDE — LET'S TALK BUTTON -->
    <div class="header-right">
      <a 
        class="talk-btn" 
        :href="whatsappLink" 
        target="_blank" 
        rel="noopener noreferrer"
      >
        Contact Me
      </a>
    </div>

  </header>
</template>

<script>
import { useRouter } from 'vue-router'

export default {
  name: "HeaderBar",

  setup() {
    const router = useRouter()
    const isActive = (path) => router.currentRoute.value.path === path

    return { isActive }
  },

  data() {
    return {
      whatsappLink: "https://wa.me/628567219006?text=Hello%20Mambuna,%20I%20would%20like%20to%20talk%20to%20you!",
    }
  }
}
</script>

<style scoped>
/* --- HEADER LAYOUT --- */
.topbar {
  width: 100%;
  padding: 24px 34px;
  display: flex;
  align-items: center;
  justify-content: space-between;
  background: rgba(0, 0, 0, 0.35);
  backdrop-filter: blur(8px);
  border-bottom: 1px solid var(--border);
}

/* LEFT SIDE BRAND */
.brand {
  display: flex;
  align-items: center;
  gap: 14px;
}

/* ROUND FLAG ICON */
.flag-circle {
  width: 40px;
  height: 40px;
  border-radius: 50%;
  overflow: hidden;
  display: flex;
  align-items: center;
  justify-content: center;
  border: 2px solid var(--accent);
  box-shadow: 0 0 12px rgba(25,209,139,0.55);
  background: rgba(25,209,139,0.10);
}

.flag-circle img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

/* MB styling */
.brand-text {
  font-weight: 900;
  font-size: 1.65rem;
  color: var(--accent);
  letter-spacing: 1.3px;
}

/* NAVIGATION */
.nav {
  display: flex;
  align-items: center;
  gap: 32px;
}

/* Base style */
.nav-item {
  position: relative;
  padding: 10px 14px;
  text-decoration: none;
  color: var(--muted);
  font-weight: 700;
  font-size: 1rem;
  transition: all .2s ease;
}

/* Hover underline glow */
.nav-item:hover::after {
  content: "";
  position: absolute;
  bottom: -4px;
  left: 0;
  width: 100%;
  height: 3px;
  background: var(--accent);
  border-radius: 2px;
  box-shadow: 0 0 14px rgba(25,209,139,0.65);
}

/* Active glowing effect */
.nav-item.active {
  color: var(--accent);
  background: rgba(25,209,139,0.12);
  padding: 10px 16px;
  border-radius: 10px;
  box-shadow: 0 0 18px rgba(25,209,139,0.35);
}

.nav-item.active:hover {
  transform: translateY(-2px);
}

/* --- LET'S TALK BUTTON (NEW) --- */
.talk-btn {
  padding: 15px 45px; /* wider */
  border-radius: 10px;
  background: rgba(25,209,139,0.18);
  border: 1px solid rgba(25,209,139,0.35);
  color: var(--accent);
  font-weight: 700;
  cursor: pointer;
  text-decoration: none;
  transition: all .25s ease;
  box-shadow: 0 0 12px rgba(25,209,139,0.25);
}

.talk-btn:hover {
  transform: translateY(-2px) scale(1.03);
  background: rgba(25,209,139,0.26);
  box-shadow: 0 0 22px rgba(25,209,139,0.45);
}
</style>
