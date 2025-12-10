<template>
  <div id="app" class="app-shell">
    <HeaderBar />
    <transition name="fade" mode="out-in">
      <router-view />
    </transition>
    <FooterBar />
  </div>
</template>

<script>
import HeaderBar from './components/HeaderBar.vue'
import FooterBar from './components/FooterBar.vue'

export default {
  name: 'App',
  components: { HeaderBar, FooterBar }
}
</script>
