<template>
  <main class="view profile-view">

    <!-- BACKGROUND GRID -->
    <div class="bg-grid"></div>

    <!-- ================= INTRO ================= -->
    <section class="profile-section reveal">
      <div class="intro-wrap">
        <h1 class="intro-title">
          Calm Exterior. Complex Mind.<br />
          Behind The <span class="accent underline">Screens</span> & Between <span class="accent underline">The Lines</span>
        </h1>

        <!-- TWO INFO BOXES -->
        <div class="intro-boxes">
          <div class="intro-box">
            <h3>Introduction</h3>
            <p>
              I am <strong>Mambuna Bojang</strong>, a quiet builder at the intersection of
               technology and thought. My work lives in software development, AI engineering, and computer networks, 
               where I enjoy turning complex ideas into efficient, reliable systems. 
               I’m naturally drawn to problem-solving that requires patience, logic, and depth rather than noise.
              Beyond code, I study people as much as systems. My interest in human behavior and psychology shapes how I think, 
              communicate, and design solutions, with intention, clarity, and balance.
            </p>
          </div>

          <div class="intro-box">
            <h3>Summary</h3>
            <p>
              Currently studying at <strong>Nusa Putra University</strong>, I’ve explored diverse areas of computing including web and mobile development, machine learning, computer networking, and GIS. 
              I thrive in calm, independent environments where focus and discipline matter most, often working late into the night refining ideas and analyzing patterns.
              I value simplicity, consistency, and meaningful growth. 
              Whether I’m optimizing a network topology, developing an application, or studying AI, 
              I approach everything with curiosity, precision, and a long-term vision: to grow into an excellent AI Engineer while building work that quietly speaks for itself.
            </p>
          </div>
        </div>
      </div>
    </section>

    <!-- ================= TECH ARSENAL ================= -->
    <section class="profile-section reveal">
      <div class="arsenal-wrap">

        <!-- PHOTO (BIGGER) -->
        <div class="arsenal-photo">
          <div class="photo-frame">
            <img :src="profileImg" alt="profile" />
          </div>
        </div>

        <!-- RIGHT SIDE -->
        <div class="arsenal-right">
          <h2 class="section-heading">Tech Arsenal</h2>

          <div class="tech-box">
            <div class="tech-grid">
              <span class="tech-item">HTML</span>
              <span class="tech-item">CSS</span>
              <span class="tech-item">JavaScript</span>
              <span class="tech-item">Vue.js</span>
              <span class="tech-item">Node.js</span>
              <span class="tech-item">Python (AI/ML)</span>
              <span class="tech-item">Git & GitHub</span>
              <span class="tech-item">Networking</span>
              <span class="tech-item">NumPY</span>
              <span class="tech-item">React-Native</span>
              <span class="tech-item">MySQL</span>
              <span class="tech-item">Linux</span>
            </div>
          </div>
        </div>

      </div>
    </section>

    <!-- ================= ACADEMIC PATH ================= -->
    <section class="profile-section reveal">
      <h2 class="section-heading">Academic Path</h2>

      <div class="academic-table">

        <div class="row">
          <div class="period">2023 — Now</div>
          <div class="context">
            <strong>Informatics Engineering Student</strong>
            <span>Nusa Putra University</span>
          </div>
          <div class="activity">
            Learn algorithms, data analysis/manipulation, AI and software engineering.
          </div>
        </div>

        <div class="row">
          <div class="period">2023 — Now</div>
          <div class="context">
            <strong>Freelance / Self-Projects</strong>
            <span>Self-Employed</span>
          </div>
          <div class="activity">
            Building responsive web applications, exploring new technologies and learning along the way
          </div>
        </div>

        <div class="row">
          <div class="period">2022 — 2023</div>
          <div class="context">
            <strong>Medical Student</strong>
            <span>University of The Gambia</span>
          </div>
          <div class="activity">
            First year medical studies focusing on basic human biology, advanced organic chemistry and basic calculus.
          </div>
        </div>

        <div class="row">
          <div class="period">2018</div>
          <div class="context">
            <strong>Science Student</strong>
            <span>Nusrat Senior Secondary School</span>
          </div>
          <div class="activity">
            Learnt basic Mathematics, Physics, Chemistry and Biology principles.
          </div>
        </div>

      </div>
    </section>

  </main>
</template>

<script>
import profileImg from '../assets/image_2.jpg'

export default {
  name: 'Profile',
  data() {
    return { profileImg }
  },
  mounted() {
    const observer = new IntersectionObserver(
      entries => {
        entries.forEach(e => e.isIntersecting && e.target.classList.add('show'))
      },
      { threshold: 0.15 }
    )
    document.querySelectorAll('.reveal').forEach(el => observer.observe(el))
  }
}
</script>

<style scoped>
/* ================= BACKGROUND GRID ================= */
.bg-grid {
  position: fixed;
  inset: 0; 
  z-index: 0;
  pointer-events: none;
  background-image:
    linear-gradient(rgba(255, 255, 255, 0.071) 1px, transparent 1px),
    linear-gradient(90deg, rgba(255, 255, 255, 0.05) 1px, transparent 1px);
  background-size: 80px 80px;
  mask-image: radial-gradient(circle at center, black 55%, transparent 100%);
}

/* ================= LAYOUT ================= */
.profile-view {
  padding: 80px 18px;
  display: flex;
  flex-direction: column;
  gap: 140px;
  position: relative;
  z-index: 1;
}

.profile-section {
  max-width: 1200px;
  margin: 0 auto;
}

/* ================= REVEAL ================= */
.reveal {
  opacity: 0;
  transform: translateY(60px);
  transition: all .8s ease;
}
.reveal.show {
  opacity: 1;
  transform: translateY(0);
}

/* ================= INTRO ================= */
.intro-title {
  font-size: 3.4rem;
  font-weight: 900;
  line-height: 1.2;
}

/* ================= ACCENT UNDERLINE + HOVER SHIMMER ================= */
.accent {
  position: relative;
  display: inline-block;
  color: #19D18B; /* make the word itself green */
  font-weight: 900;
  transition: color .22s ease;
}
/* solid green underline that spans the full width of the span */
.accent::after {
  content: "";
  position: absolute;
  left: 0;
  right: 0;
  bottom: -6px;
  height: 5px;
  background: #19D18B; /* solid beautiful green */
  border-radius: 2px;
  opacity: 1;
  transform-origin: left;
  transition: height .28s cubic-bezier(.2,.9,.3,1), opacity .25s;
  pointer-events: none;
}

.accent::before {
  content: "";
  position: absolute;
  inset: -8px;
  border-radius: 10px;
  background: conic-gradient(#19D18B44, #19D18B88, #19D18B33, #19D18B88, #19D18B44);
  filter: blur(10px);
  opacity: 0;
  transform: scale(.98);
  transition: opacity .35s, transform .45s;
  z-index: -1;
  pointer-events: none;
}
.accent:hover::before,
.accent:focus::before {
  opacity: 1;
  transform: scale(1);
  animation: spinGlow 1.8s linear infinite;
}
.accent:hover::after,
.accent:focus::after {
  height: 12px;
  opacity: 1;
}
@keyframes spinGlow {
  from { transform: scale(1) rotate(0deg); }
  to   { transform: scale(1) rotate(360deg); }
}

.underline { text-decoration: none; }

.intro-boxes {
  margin-top: 40px;
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 28px;
}

.intro-box {
  padding: 28px;
  border-radius: 18px;
  background: rgba(255,255,255,0.03);
  border: 1px solid rgba(255,255,255,0.06);
  color: var(--muted);
  transition: all .3s ease;
}
.intro-box h3 {
  margin-bottom: 12px;
}
.intro-box:hover {
  color: #fff;
  transform: translateY(-6px);
  box-shadow: 0 0 40px rgba(25,209,139,0.25);
}

/* ================= TECH ARSENAL ================= */
.section-heading {
  font-size: 2.2rem;
  font-weight: 800;
  margin-bottom: 24px;
}

.arsenal-wrap {
  display: grid;
  grid-template-columns: 420px 1fr;
  gap: 60px;
  align-items: center;
}

/* Photo */
.photo-frame {
  width: 100%;
  aspect-ratio: 3 / 4;
  border-radius: 20px;
  overflow: hidden;
  border: 1px solid rgba(25,209,139,0.25);
  box-shadow: 0 0 50px rgba(25,209,139,0.15);
  transition: all .4s ease;
}
.photo-frame img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  filter: grayscale(100%);
  transition: all .4s ease;
}
.photo-frame:hover img {
  filter: grayscale(0%);
  transform: scale(1.06);
}
.photo-frame:hover {
  box-shadow: 0 0 90px rgba(25,209,139,0.45);
}

/* Tech grid */
.tech-box {
  background: rgba(255,255,255,0.03);
  border: 1px solid rgba(255,255,255,0.06);
  border-radius: 20px;
  padding: 28px;
}
.tech-grid {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 16px;
}
.tech-item {
  position: relative;
  z-index: 0;
  padding: 14px;
  text-align: center;
  font-weight: 700;
  border-radius: 12px;
  background: rgba(255,255,255,0.03);
  border: 1px solid rgba(255,255,255,0.06);
  transition: all .25s ease;
  overflow: visible;
}
/* subtle static green glow on hover (no spinning) */
.tech-item::before {
  content: "";
  position: absolute;
  inset: -6px;
  border-radius: 14px;
  background: radial-gradient(circle at center, rgba(25,209,139,0.12), rgba(25,209,139,0.04) 40%, transparent 60%);
  filter: blur(10px);
  opacity: 0;
  transform: scale(.98);
  transition: opacity .35s, transform .35s;
  z-index: -1;
  pointer-events: none;
}
/* sweeping underline (different animation) */
.tech-item::after {
  content: "";
  position: absolute;
  left: 8%;
  right: 8%;
  bottom: -8px;
  height: 5px;
  background: linear-gradient(90deg, rgba(25,209,139,0), #19D18B, rgba(25,209,139,0));
  background-size: 200% 100%;
  transform: scaleX(0);
  transform-origin: left;
  transition: transform .35s cubic-bezier(.2,.9,.3,1), opacity .25s;
  opacity: 0;
  border-radius: 3px;
  z-index: -1;
}
.tech-item:hover::before {
  opacity: 1;
  transform: scale(1);
}
.tech-item:hover::after {
  opacity: 1;
  transform: scaleX(1);
  animation: techSweep 0.9s linear;
}
.tech-item:hover {
  color: #eafff6;
  transform: translateY(-6px);
  box-shadow: 0 0 22px rgba(25,209,139,0.35);
}

@keyframes techSweep {
  0% { background-position: 0% 50%; }
  100% { background-position: 100% 50%; }
}
.section-heading {
  font-size: 2.2rem;
  font-weight: 800;
  margin-bottom: 24px;
}

.arsenal-wrap {
  display: grid;
  grid-template-columns: 420px 1fr;
  gap: 60px;
  align-items: center;
}

/* Photo */
.photo-frame {
  width: 100%;
  aspect-ratio: 3 / 4;
  border-radius: 20px;
  overflow: hidden;
  border: 1px solid rgba(25,209,139,0.25);
  box-shadow: 0 0 50px rgba(25,209,139,0.15);
  transition: all .4s ease;
}
.photo-frame img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  filter: grayscale(100%);
  transition: all .4s ease;
}
.photo-frame:hover img {
  filter: grayscale(0%);
  transform: scale(1.06);
}
.photo-frame:hover {
  box-shadow: 0 0 90px rgba(25,209,139,0.45);
}

/* Tech grid */
.tech-box {
  background: rgba(255,255,255,0.03);
  border: 1px solid rgba(255,255,255,0.06);
  border-radius: 20px;
  padding: 28px;
}
.tech-grid {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 16px;
}
.tech-item {
  position: relative;
  z-index: 0;
  padding: 14px;
  text-align: center;
  font-weight: 700;
  border-radius: 12px;
  background: rgba(255,255,255,0.03);
  border: 1px solid rgba(255,255,255,0.06);
  transition: all .25s ease;
  overflow: visible;
}
.tech-item::before {
  content: "";
  position: absolute;
  inset: -8px;
  border-radius: 16px;
  background: conic-gradient(#19D18B00, #19D18B33, #19D18B99, #19D18B33, #19D18B00);
  filter: blur(8px);
  opacity: 0;
  transform: scale(.95);
  transition: opacity .35s, transform .45s;
  z-index: -1;
  pointer-events: none;
}
.tech-item:hover::before {
  opacity: 1;
  transform: scale(1);
  animation: spinGlow 1.8s linear infinite;
}
.tech-item:hover {
  color: #eafff6;
  transform: translateY(-6px);
  box-shadow: 0 0 22px rgba(25,209,139,0.35);
}

/* ================= ACADEMIC TABLE ================= */
.academic-table {
  display: flex;
  flex-direction: column;
}
.row {
  display: grid;
  grid-template-columns: 140px 320px 1fr;
  padding: 22px 12px;
  border-top: 1px solid rgba(255,255,255,0.06);
  transition: all .3s ease;
}
.row:last-child {
  border-bottom: 1px solid rgba(255,255,255,0.06);
}
.row:hover {
  transform: translateX(10px);
}
.row:hover .period,
.row:hover .context strong {
  color: var(--accent);
}
.period {
  color: var(--muted);
  transition: color .25s;
}
.context strong {
  display: block;
  transition: color .25s;
}
.context span,
.activity {
  color: var(--muted);
}

/* ================= RESPONSIVE ================= */
@media (max-width: 900px) {
  .intro-boxes {
    grid-template-columns: 1fr;
  }
  .arsenal-wrap {
    grid-template-columns: 1fr;
  }
  .tech-grid {
    grid-template-columns: repeat(2, 1fr);
  }
  .row {
    grid-template-columns: 1fr;
    gap: 8px;
  }
}
</style>
