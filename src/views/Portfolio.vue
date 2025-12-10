<template>
  <main class="view portfolio-view">
    <div class="portfolio-header">
      <h2>Portfolio</h2>
      <p class="muted">Certificates / Experience / Projects — interactive showcase</p>

      <div class="tab-row" role="tablist" aria-label="Portfolio sections">
        <button v-for="t in tabs" :key="t" @click="select(t)" :class="['tab-btn', {active: t===current}]" >
          {{ t }}
        </button>
      </div>
    </div>

    <section class="portfolio-body">
      <transition name="slide-fade" mode="out-in">
        <component :is="currentComponent" :key="current" />
      </transition>
    </section>
  </main>
</template>

<script>
import Certificates from '../components/Certificates.vue'
import Experience from '../components/Experience.vue'
import Projects from '../components/Projects.vue'

export default {
  name: 'Portfolio',
  components: { Certificates, Experience, Projects },
  data() {
    return {
      tabs: ['Certificates','Experience','Projects'],
      current: 'Certificates'
    }
  },
  computed: {
    currentComponent() {
      return this.current.replace(/\s/g,'') // Certificates -> Certificates (component name)
    }
  },
  methods: {
    select(t){ this.current = t }
  }
}
</script>
