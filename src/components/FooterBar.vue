<template>
  <footer class="site-footer">
    <div class="footer-inner">
      <!-- Column 1: Name & Role -->
      <div class="footer-col name-col">
        <div class="name-block">
          <div class="hero-name-footer">
            <span class="first-name">{{ firstName }}</span>
            <span class="last-name">{{ lastName }}</span>
          </div>
          <div class="role">Full Stack Developer</div>
        </div>
      </div>

      <!-- Column 2: Connect -->
      <div class="footer-col connect-col" aria-label="connect">
        <h4>CONNECT</h4>
        <nav class="connect-list">
          <a :href="linkedin" class="connect-item" target="_blank" rel="noopener noreferrer">
            <span class="icon" v-html="icons.linkedin"></span>
            <span class="label">LinkedIn</span>
          </a>

          <a :href="github" class="connect-item" target="_blank" rel="noopener noreferrer">
            <span class="icon" v-html="icons.github"></span>
            <span class="label">GitHub</span>
          </a>

          <a :href="`mailto:${email}`" class="connect-item">
            <span class="icon" v-html="icons.mail"></span>
            <span class="label">Email</span>
          </a>

          <a :href="cvLink" class="connect-item" target="_blank" rel="noopener noreferrer">
            <span class="icon" v-html="icons.cv"></span>
            <span class="label">CV</span>
          </a>
        </nav>
      </div>

      <!-- Column 3: Sitemap -->
      <div class="footer-col sitemap-col" aria-label="sitemap">
        <h4>SITEMAP</h4>
        <nav class="sitemap-list">
          <router-link class="sitemap-link" to="/">Home</router-link>
          <router-link class="sitemap-link" to="/about">About</router-link>
          <router-link class="sitemap-link" to="/portfolio">Portfolio</router-link>
        </nav>
      </div>
    </div>
  </footer>
</template>

<script>
export default {
  name: 'FooterBar',
  data() {
    return {
      year: new Date().getFullYear(),
      firstName: 'MAMBUNA',
      lastName: 'BOJANG',
      email: 'federiconacamora2099@gmail.com',
      linkedin: 'https://www.linkedin.com/in/mambuna-bojang-b800b72a6',
      github: 'https://github.com/FedericoMel20',
      cvLink: '/CV-Mambuna.pdf',
      icons: {
        linkedin: `<svg viewBox="0 0 24 24" width="22" height="22" fill="currentColor" xmlns="http://www.w3.org/2000/svg"><path d="M4.98 3.5C4.98 4.6 4.06 5.5 2.96 5.5 1.86 5.5.94 4.6.94 3.5.94 2.4 1.86 1.5 2.96 1.5 4.06 1.5 4.98 2.4 4.98 3.5zM.9 8.98h4.12V24H.9V8.98zM9.9 8.98h3.95v2.02h.06c.55-1.04 1.9-2.14 3.9-2.14 4.17 0 4.94 2.75 4.94 6.33V24h-4.12v-7.7c0-1.84-.03-4.2-2.56-4.2-2.56 0-2.95 2-2.95 4.06V24H9.9V8.98z"/></svg>`,
        github: `<svg viewBox="0 0 24 24" width="22" height="22" fill="currentColor" xmlns="http://www.w3.org/2000/svg"><path d="M12 .5C5.65.5.5 5.65.5 12c0 5.09 3.29 9.42 7.86 10.95.58.11.79-.25.79-.56 0-.27-.01-1-.02-1.96-3.2.7-3.88-1.38-3.88-1.38-.53-1.36-1.3-1.72-1.3-1.72-1.06-.72.08-.71.08-.71 1.17.08 1.78 1.2 1.78 1.2 1.04 1.77 2.73 1.26 3.39.96.11-.75.41-1.26.75-1.55-2.56-.29-5.25-1.28-5.25-5.7 0-1.26.45-2.29 1.19-3.09-.12-.29-.52-1.45.11-3.02 0 0 .97-.31 3.18 1.18A11.1 11.1 0 0112 6.8c.98.004 1.97.133 2.89.39 2.2-1.5 3.17-1.18 3.17-1.18.63 1.57.23 2.73.11 3.02.74.8 1.19 1.83 1.19 3.09 0 4.43-2.7 5.41-5.27 5.69.42.36.8 1.08.8 2.18 0 1.57-.015 2.84-.015 3.23 0 .31.21.68.8.56C20.71 21.42 24 17.09 24 12c0-6.35-5.15-11.5-12-11.5z"/></svg>`,
        mail: `<svg viewBox="0 0 24 24" width="22" height="22" fill="currentColor" xmlns="http://www.w3.org/2000/svg"><path d="M20 4H4a2 2 0 0 0-2 2v12a2 2 0 0 0 2 2h16a2 2 0 0 0 2-2V6a2 2 0 0 0-2-2zm0 4l-8 5-8-5V6l8 5 8-5v2z"/></svg>`,
        cv: `<svg viewBox="0 0 24 24" width="22" height="22" fill="currentColor" xmlns="http://www.w3.org/2000/svg"><path d="M14 2H6a2 2 0 0 0-2 2v16c0 1.1.9 2 2 2h12a2 2 0 0 0 2-2V8l-6-6zm1 7V3.5L20.5 9H15zM8 12h8v2H8v-2zm0 4h8v2H8v-2z"/></svg>`
      }
    }
  }
}
</script>

<style scoped>
.site-footer {
  border-top: 1px solid rgba(25,209,139,0.15);
  background: linear-gradient(
      180deg,
      rgba(0, 30, 22, 0.35),
      rgba(0, 45, 32, 0.25),
      rgba(0, 60, 42, 0.20)
  );
  
  /* soft green inner glow */
  box-shadow: inset 0 0 35px rgba(25,209,139,0.08);

  padding: 28px;
  color: var(--muted);
  backdrop-filter: blur(4px);
}

.footer-inner {
  max-width: 1200px;
  margin: 0 auto;
  display: grid;
  grid-template-columns: 1fr 360px 220px;
  gap: 24px;
  align-items: start;
}
/* Name column */
.name-col .name-block { margin-bottom: 12px; }
.hero-name-footer { font-weight: 900; font-size: 1.35rem; color: #fff; line-height: 1; }
.hero-name-footer .first-name { display:block; }
.hero-name-footer .last-name { display:block; margin-left: 3ch; /* starts roughly at 4th char of first name */ }
/* role text */
.role { color: var(--accent); font-weight:700; margin-top:8px; font-size:0.95rem; }

/* Connect column */
.connect-col h4, .sitemap-col h4 { color: var(--muted); margin: 0 0 10px 0; letter-spacing: 0.6px; font-weight:700; }
.connect-list {
  display:flex; flex-direction:column; gap:10px;
}
.connect-item {
  display:flex; align-items:center; gap:12px; text-decoration:none; color:var(--muted);
  padding:8px; border-radius:10px; transition: all .2s ease;
}
.connect-item .icon { width:40px; height:40px; display:inline-flex; align-items:center; justify-content:center; color:var(--accent); background:transparent; border-radius:8px; }
.connect-item .icon svg { width:22px; height:22px; display:block; color: inherit; }
.connect-item .label { font-weight:700; color:var(--muted); }

/* Hover effect: glow & accent color */
.connect-item:hover {
  background: linear-gradient(90deg, rgba(25,209,139,0.06), rgba(0,194,168,0.03));
  box-shadow: 0 12px 40px rgba(25,209,139,0.08);
  transform: translateX(4px)
}
.connect-item:hover .label { color: var(--accent); }
.connect-item:hover .icon { box-shadow: 0 6px 30px rgba(25,209,139,0.07); background: rgba(25,209,139,0.03); color:var(--accent); }

/* Sitemap column */
.sitemap-list { display:flex; flex-direction:column; gap:8px; }
.sitemap-link {
  display:inline-block; padding:8px 10px; border-radius:8px; color:var(--muted); text-decoration:none; font-weight:700;
  transition: all .18s;
}
.sitemap-link:hover {
  background: linear-gradient(90deg, rgba(25,209,139,0.06), rgba(0,194,168,0.02)); color:var(--accent);
  transform: translateX(4px);
}

/* copyright */
.copyright { margin-top:12px; color:var(--muted); font-size:0.85rem; }

/* Responsive */
@media (max-width:980px) {
  .footer-inner { grid-template-columns: 1fr; gap:14px; }
  .hero-name-footer { font-size:1.1rem }
  .connect-item { padding:10px 6px; gap:8px; }
  .connect-item .icon { width:36px; height:36px; }
}
</style>
