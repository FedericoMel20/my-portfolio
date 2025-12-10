<template>
  <div class="subsection certificates">
    <h3>Certificates</h3>
    <div class="cards">
      <article class="mini-card" v-for="n in 4" :key="n">
        <div class="mini-head">Cert {{ n }}</div>
        <p class="mini-desc">Issuer • Course name • Year</p>
        <div class="card-actions">
          <button class="ghost">View</button>
          <button class="ghost">Download</button>
        </div>
      </article>
    </div>
  </div>
</template>

<script>
export default { name: 'Certificates' }
</script>
