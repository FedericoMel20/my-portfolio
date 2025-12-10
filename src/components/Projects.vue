<template>
  <div class="subsection projects">
    <h3>Projects</h3>
    <div class="projects-grid">
      <article class="project-card" v-for="p in projects" :key="p.id" @mousemove="tilt($event,$event.currentTarget)" @mouseleave="reset($event.currentTarget)">
        <div class="project-media"></div>
        <div class="project-body">
          <h4>{{ p.title }}</h4>
          <p class="muted">{{ p.tags.join(' • ') }}</p>
          <p>{{ p.description }}</p>
          <div class="actions">
            <a :href="p.link" target="_blank" rel="noreferrer" class="btn">Open</a>
          </div>
        </div>
      </article>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Projects',
  data() {
    return {
      projects: [
        { id:1, title:'Network Dashboard', tags:['Vue','Socket'], description:'Realtime monitoring dashboard', link:'#' },
        { id:2, title:'Portfolio Site', tags:['Vue','Vite'], description:'This site you see', link:'#' }
      ]
    }
  },
  methods: {
    tilt(e, el) {
      const rect = el.getBoundingClientRect()
      const x = (e.clientX - rect.left) / rect.width - 0.5
      const y = (e.clientY - rect.top) / rect.height - 0.5
      const rotY = x * 8
      const rotX = -y * 8
      el.style.transform = `rotateX(${rotX}deg) rotateY(${rotY}deg) scale(1.02)`
    },
    reset(el) { el.style.transform = '' }
  }
}
</script>
