<template>
  <div class="subsection experience">
    <h3>Experience</h3>
    <ul class="timeline">
      <li v-for="(it,i) in items" :key="i" class="timeline-item">
        <div class="dot"></div>
        <div class="content">
          <h4>{{ it.role }}</h4>
          <p class="muted">{{ it.company }} • {{ it.period }}</p>
          <p>{{ it.desc }}</p>
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'Experience',
  data() {
    return {
      items: [
        { role:'Frontend Dev', company:'Company A', period:'2023 — Present', desc:'Built SPAs and dashboards' },
        { role:'Network Engineer', company:'Org X', period:'2021 — 2023', desc:'Managed infra and monitoring' }
      ]
    }
  }
}
</script>
