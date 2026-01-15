<template>
  <header class="topbar">
    
    <!-- LEFT SIDE: FLAG + MB -->
    <div class="brand">
      <div class="flag-circle">
        <img src="/gambia-flag.png" alt="Gambian Flag" />
      </div>
      <span class="brand-text">MB</span>
    </div>

    <!-- HAMBURGER MENU (MOBILE) -->
    <button class="hamburger" @click="mobileMenuOpen = !mobileMenuOpen" :class="{ active: mobileMenuOpen }" aria-label="Toggle menu">
      <span></span>
      <span></span>
      <span></span>
    </button>

    <!-- NAVIGATION -->
    <nav class="nav" :class="{ open: mobileMenuOpen }">
      <router-link 
        to="/" 
        class="nav-item" 
        :class="{ active: isActive('/') }"
        @click="mobileMenuOpen = false">
        HOME
      </router-link>

      <router-link 
        to="/profile" 
        class="nav-item" 
        :class="{ active: isActive('/profile') }"
        @click="mobileMenuOpen = false">
        PROFILE
      </router-link>

      <router-link 
        to="/portfolio" 
        class="nav-item" 
        :class="{ active: isActive('/portfolio') }"
        @click="mobileMenuOpen = false">
        PORTFOLIO
      </router-link>
    </nav>

    <!-- RIGHT SIDE — LET'S TALK BUTTON -->
    <div class="header-right">
      <button 
        class="talk-btn" 
        @click="showTalkModal = true"
        aria-haspopup="dialog"
      >
        Contact Me
      </button>

      <TalkModal v-if="showTalkModal" @close="showTalkModal = false" />
    </div>

  </header>
</template>

<script>
import { useRouter } from 'vue-router'
import TalkModal from './TalkModal.vue'

export default {
  name: "HeaderBar",
  components: { TalkModal },

  setup() {
    const router = useRouter()
    const isActive = (path) => router.currentRoute.value.path === path

    return { isActive }
  },

  data() {
    return {
      showTalkModal: false,
      mobileMenuOpen: false,
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
  position: relative;
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

/* HAMBURGER MENU (MOBILE) */
.hamburger {
  display: none;
  flex-direction: column;
  background: transparent;
  border: none;
  cursor: pointer;
  gap: 6px;
  padding: 8px;
  z-index: 1001;
}

.hamburger span {
  width: 24px;
  height: 3px;
  background: var(--accent);
  border-radius: 2px;
  transition: all 0.3s ease;
  display: block;
}

.hamburger.active span:nth-child(1) {
  transform: rotate(45deg) translate(10px, 10px);
}

.hamburger.active span:nth-child(2) {
  opacity: 0;
}

.hamburger.active span:nth-child(3) {
  transform: rotate(-45deg) translate(7px, -7px);
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
  padding: 15px 45px;
  border-radius: 10px;
  background: rgba(25,209,139,0.18);
  border: 1px solid rgba(25,209,139,0.35);
  color: var(--accent);
  font-weight: 700;
  cursor: pointer;
  text-decoration: none;
  transition: all .25s ease;
  box-shadow: 0 0 12px rgba(25,209,139,0.25);
  white-space: nowrap;
}

.talk-btn:hover {
  transform: translateY(-2px) scale(1.03);
  background: rgba(25,209,139,0.26);
  box-shadow: 0 0 22px rgba(25,209,139,0.45);
}

/* --- MOBILE RESPONSIVE --- */
@media (max-width: 1024px) {
  .topbar {
    padding: 18px 24px;
  }

  .brand-text {
    font-size: 1.5rem;
  }

  .nav {
    gap: 24px;
  }

  .nav-item {
    font-size: 0.95rem;
    padding: 10px 12px;
  }

  .talk-btn {
    padding: 12px 32px;
    font-size: 0.95rem;
  }
}

@media (max-width: 768px) {
  .topbar {
    padding: 16px 18px;
  }

  .brand-text {
    font-size: 1.3rem;
  }

  .hamburger {
    display: flex;
  }

  .nav {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100vh;
    background: linear-gradient(135deg, rgba(7, 16, 24, 0.98), rgba(8, 20, 26, 0.98));
    backdrop-filter: blur(12px);
    flex-direction: column;
    gap: 20px;
    align-items: center;
    justify-content: center;
    transform: translateX(-100%);
    transition: transform 0.3s ease;
    z-index: 1000;
  }

  .nav.open {
    transform: translateX(0);
  }

  .nav-item {
    font-size: 1.3rem;
    padding: 16px 24px;
    border-radius: 12px;
    text-align: center;
    width: 75%;
    transition: all 0.3s ease;
  }

  .nav-item:hover {
    background: rgba(25, 209, 139, 0.15);
    transform: scale(1.03);
  }

  .nav-item.active {
    background: linear-gradient(90deg, rgba(25,209,139,0.25), rgba(0,194,168,0.15));
    box-shadow: 0 0 30px rgba(25,209,139,0.45);
    transform: scale(1.05);
  }

  .nav-item::after {
    display: none;
  }

  .header-right {
    display: flex;
  }

  .talk-btn {
    padding: 12px 28px;
    font-size: 0.95rem;
    white-space: nowrap;
  }
}

@media (max-width: 480px) {
  .topbar {
    padding: 14px 14px;
  }

  .flag-circle {
    width: 36px;
    height: 36px;
    border: 2px solid var(--accent);
  }

  .brand-text {
    font-size: 1.1rem;
  }

  .hamburger span {
    width: 22px;
    height: 2.5px;
  }

  .nav-item {
    font-size: 1.1rem;
    padding: 14px 20px;
  }

  .talk-btn {
    padding: 10px 20px;
    font-size: 0.85rem;
  }
}
</style>
