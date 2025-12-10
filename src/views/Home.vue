<template>
  <main class="view home-view hero-centered">
    <section class="hero-area">
      <div class="hero-content">
        <div class="hero-text">
          <div class="hero-name-large">
            <span class="first-name">{{ firstName }}</span>
            <span class="last-name">{{ lastName }}</span>
          </div>
          <p class="hero-subtitle">Full Stack Developer</p>
        </div>

        <div class="hero-portrait">
          <div class="portrait-frame big">
            <div class="portrait-inner">
              <img :src="avatar" alt="avatar" class="avatar" />
            </div>
            <div class="portrait-ornament"></div>
          </div>
        </div>
      </div>
    </section>
  </main>
</template>

<script>
import avatarImg from '../assets/image_1.jpg'
export default {
  name: 'Home',
  data() {
    return {
      firstName: 'Mambuna',
      lastName: 'Bojang',
      avatar: avatarImg
    }
  }
}
</script>

<style scoped>
.hero-centered { display:flex; justify-content:center; align-items:center; padding:48px 18px; }

.hero-area { width:100%; max-width:1100px; }

.hero-content { display:flex; align-items:center; justify-content:space-between; gap:40px; }

/* Name block */
.hero-text { flex:1; display:flex; flex-direction:column; justify-content:center; align-items:flex-start; padding-left:18px; }
.hero-name-large { color: #fff; font-weight:900; font-size:4.2rem; line-height:0.9; letter-spacing:1px; }
.hero-name-large .first-name { display:block; }
.hero-name-large .last-name { display:block; margin-left: 3ch; /* starts roughly at 4th char of first name */ }
.hero-subtitle { margin-top:12px; color:var(--accent); font-weight:700; font-size:1.05rem; }

/* Portrait */
.hero-portrait { width:420px; display:flex; justify-content:center; align-items:center; }
.portrait-frame.big { width:420px; height:420px; border-radius:20px; padding:20px; }
.portrait-inner { width:300px; height:300px; border-radius:50%; overflow:hidden; display:flex; align-items:center; justify-content:center; background: radial-gradient(circle at 20% 20%, rgba(25,209,139,0.06), transparent 25%); border:1px solid rgba(25,209,139,0.08); transition: transform .38s; }
.portrait-inner .avatar { width:100%; height:100%; object-fit:cover; }
.portrait-frame.big:hover .portrait-inner { transform: scale(1.04) rotate(-1.6deg); box-shadow: 0 30px 100px rgba(0,200,150,0.06); }

/* Responsiveness */
@media (max-width:980px) {
  .hero-content { flex-direction:column-reverse; gap:18px; align-items:center; text-align:center; }
  .hero-text { align-items:center; padding-left:0; }
  .hero-name-large { font-size:3rem; }
  .portrait-frame.big { width:280px; height:280px; padding:14px; }
  .portrait-inner { width:200px; height:200px; }
}
</style>
