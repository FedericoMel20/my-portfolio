<template>
  <header class="topbar">
    <div class="brand">
      <div class="logo"></div>
      <span class="brand-text">DIGITAL CANVAS</span>
    </div>

    <nav class="nav">
      <router-link to="/" class="nav-item" :class="{active:isActive('/')}" >HOME</router-link>
      <router-link to="/profile" class="nav-item" :class="{active:isActive('/profile')}">PROFILE</router-link>
      <router-link to="/portfolio" class="nav-item" :class="{active:isActive('/portfolio')}">PORTFOLIO</router-link>
    </nav>

    <div class="header-right">
      <button class="icon-btn" title="menu">≡</button>
    </div>
  </header>
</template>

<script>
import { useRouter } from 'vue-router'
export default {
  name: 'HeaderBar',
  setup() {
    const router = useRouter()
    const isActive = (path) => router.currentRoute.value.path === path
    return { isActive }
  }
}
</script>
