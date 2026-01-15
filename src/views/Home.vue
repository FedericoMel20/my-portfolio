<template>
  <main class="view home-view hero-centered">
    <!-- Visible curved background fixed to bottom-right -->
    <div class="bg-curve" aria-hidden="true"></div>

    <section class="hero-area">
      <div class="hero-content">

        <!-- LEFT SIDE: NAME -->
        <div class="hero-text">
          <div class="hero-name-large">
            <span class="first-name">{{ firstName }}</span>
            <span class="last-name">{{ lastName }}</span>
          </div>
          <p class="hero-subtitle">Full Stack Developer</p>
        </div>

        <!-- RIGHT SIDE: PORTRAIT + DESCRIPTION -->
        <div class="hero-portrait">
          <div class="portrait-frame big">
            <div class="portrait-inner">
              <img :src="avatar" alt="avatar" class="avatar" />
            </div>
            <div class="portrait-ornament"></div>
          </div>

          <!-- NEW TEXT UNDER PHOTO -->
          <div class="hero-description">
            Informatics Engineering Student <br />
            Nusa Putra University
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
      firstName: 'MAMBUNA',
      lastName: 'BOJANG',
      avatar: avatarImg
    }
  }
}
</script>

<style scoped>
/* ---------- quick tweakable variables ---------- */
:root {
  --corner-left: 12px;     /* change to 6px / 20px to tune corner mark inset */
  --leaf: #19d18b;
  --leaf-strong: #00c76b;
}

/* -------------------------
   Layout & hero content
   ------------------------- */

.hero-centered {
  display:flex;
  justify-content:center;
  align-items:center;
  padding:48px 18px;
  position: relative; /* important for content stacking */
  isolation: isolate; /* ensure stacking context for fixed bg */
  overflow: visible;
}

.hero-area {
  width:100%;
  max-width:1100px;
  z-index: 3; /* place above background */
}

.hero-content {
  display:flex;
  align-items:center;
  justify-content:space-between;
  gap:40px;
  position: relative;
}

/* Name block */
.hero-text {
  flex:1;
  display:flex;
  flex-direction:column;
  justify-content:center;
  align-items:flex-start;
  padding-left:18px;
}

.hero-name-large {
  color: #fff;
  font-weight: 900;
  font-size: 5rem;
  line-height: 0.9;
  letter-spacing: 1.2px;
}

.hero-name-large .first-name { display: block; }

.hero-name-large .last-name {
  display: block;
  margin-left: 4ch; /* last name starts under 5th char of first name */
}

.hero-subtitle {
  margin-top: 14px;
  margin-left: 4ch;
  color: var(--accent);
  font-weight: 700;
  font-size: 1.25rem;
  letter-spacing: 0.6px;
}

/* Portrait */
.hero-portrait {
  width:420px;
  display:flex;
  flex-direction:column;
  justify-content:center;
  align-items:center;
  position: relative;
}

.portrait-frame.big {
  width:420px;
  height:420px;
  border-radius:20px;
  padding:20px;
  background: linear-gradient(180deg, rgba(255,255,255,0.01), rgba(0,0,0,0.02));
  border: 1px solid rgba(255,255,255,0.02);
}

.portrait-inner {
  width:300px;
  height:300px;
  border-radius:50%;
  overflow:hidden;
  display:flex;
  align-items:center;
  justify-content:center;
  background: radial-gradient(circle at 20% 20%, rgba(25,209,139,0.06), transparent 25%);
  border:1px solid rgba(25,209,139,0.08);
  transition: transform .38s;
}

.portrait-inner .avatar {
  width:100%;
  height:100%;
  object-fit:cover;
}

.portrait-frame.big:hover .portrait-inner {
  transform: scale(1.04) rotate(-1.6deg);
  box-shadow: 0 30px 100px rgba(0,200,150,0.06);
}

/* hero description */
.hero-description {
  margin-top: 18px;
  text-align: center;
  font-size: 1.1rem;
  font-weight: 600;
  color: #ffffff;
  letter-spacing: 0.5px;
  transition: all .25s ease;
  padding: 8px 14px;
  border: 1px solid rgba(255,255,255,0.06);
  border-radius: 20px;
  display: inline-block;
}

.hero-description:hover {
  color: var(--accent);
  transform: translateY(-4px);
  box-shadow: 0 0 18px rgba(25,209,139,0.35),
              0 0 6px rgba(25,209,139,0.25) inset;
  border: 1px solid rgba(25,209,139,0.35);
  cursor: default;
}

/* -------------------------
   Curved bottom-right background (fixed & visible)
   ------------------------- */

/* Simple, guaranteed-visible curved background fixed to viewport bottom-right */
.bg-curve {
  position: fixed;
  right: 0;
  bottom: 0;
  width: 50vw;        /* visible width - tweak as desired */
  height: 45vh;       /* height of the sweep */
  z-index: 1;         /* behind hero content (z-index smaller than .hero-area) */
  pointer-events: none;

  background: radial-gradient(
    circle at 80% 80%,
    rgba(25, 209, 139, 0.36) 0%,
    rgba(10, 80, 55, 0.40) 30%,
    rgba(6, 50, 40, 0.32) 55%,
    rgba(0, 0, 0, 0) 100%
  );

  /* soft rounded sweep */
  border-bottom-left-radius: 60%;
  box-shadow: inset -120px -20px 160px rgba(0, 120, 80, 0.12), 0 30px 120px rgba(4,120,86,0.06);
  filter: saturate(112%) blur(0.1px);
  transform: translateZ(0);
  opacity: 0.95;
}

/* Smaller screens adjustments for the curve */
@media (max-width:1200px) {
  .bg-curve {
    width: 70vw;
    height: 42vh;
    box-shadow: inset -100px -10px 120px rgba(0,120,80,0.10), 0 20px 100px rgba(4,120,86,0.05);
  }
}

@media (max-width:1024px) {
  .hero-centered {
    padding: 48px 18px;
  }

  .hero-content {
    gap: 30px;
  }

  .hero-name-large {
    font-size: 4rem;
  }

  .hero-subtitle {
    font-size: 1.15rem;
  }

  .hero-portrait {
    width: 360px;
  }

  .portrait-frame.big {
    width: 360px;
    height: 360px;
  }

  .portrait-inner {
    width: 260px;
    height: 260px;
  }
}

@media (max-width:980px) {
  .bg-curve {
    right: -8vw;
    bottom: -6vh;
    width: 120vw;
    height: 38vh;
    opacity: 0.85;
  }

  .hero-content {
    gap: 18px;
  }
  .hero-portrait {
    width: 320px;
  }
  .portrait-frame.big {
    width: 320px;
    height: 320px;
    padding: 16px;
  }
  .portrait-inner {
    width: 220px;
    height: 220px;
  }
  .hero-name-large {
    font-size: 3.2rem;
  }
}

@media (max-width: 768px) {
  .hero-centered {
    padding: 32px 14px;
    min-height: 85vh;
  }

  .hero-content {
    gap: 16px;
    flex-direction: row;
    align-items: center;
    justify-content: space-between;
  }

  .hero-text {
    flex: 1;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: flex-start;
    padding-left: 0;
    min-width: 0;
  }

  .hero-name-large {
    font-size: 2rem;
    line-height: 0.95;
    word-break: break-word;
  }

  .hero-name-large .first-name {
    display: inline;
  }

  .hero-name-large .last-name {
    display: inline;
    margin-left: 0;
  }

  .hero-subtitle {
    margin-left: 0;
    font-size: 0.95rem;
    margin-top: 6px;
  }

  .hero-portrait {
    width: 200px;
    flex-shrink: 0;
  }

  .portrait-frame.big {
    width: 200px;
    height: 200px;
    padding: 12px;
  }

  .portrait-inner {
    width: 140px;
    height: 140px;
  }

  .hero-description {
    font-size: 0.8rem;
    margin-top: 8px;
    padding: 6px 10px;
  }

  .bg-curve {
    width: 100vw;
    height: 30vh;
    right: 0;
    bottom: 0;
  }

  .corner-mark {
    display: none;
  }
}

@media (max-width: 480px) {
  .hero-centered {
    padding: 24px 12px;
    min-height: 80vh;
  }

  .hero-content {
    gap: 12px;
    flex-direction: row;
    align-items: center;
  }

  .hero-text {
    flex: 1;
    min-width: 0;
  }

  .hero-name-large {
    font-size: 1.4rem;
    line-height: 1;
  }

  .hero-name-large .first-name {
    display: inline;
  }

  .hero-name-large .last-name {
    display: inline;
    margin-left: 0;
  }

  .hero-subtitle {
    font-size: 0.8rem;
    margin-top: 4px;
  }

  .hero-portrait {
    width: 140px;
    flex-shrink: 0;
  }

  .portrait-frame.big {
    width: 140px;
    height: 140px;
    padding: 8px;
  }

  .portrait-inner {
    width: 100px;
    height: 100px;
  }

  .hero-description {
    font-size: 0.7rem;
    margin-top: 6px;
    padding: 5px 8px;
  }

  .bg-curve {
    height: 25vh;
    opacity: 0.6;
  }
}

@media (max-width: 360px) {
  .hero-content {
    gap: 8px;
  }

  .hero-portrait {
    width: 120px;
  }

  .portrait-frame.big {
    width: 120px;
    height: 120px;
    padding: 6px;
  }

  .portrait-inner {
    width: 85px;
    height: 85px;
  }

  .hero-name-large {
    font-size: 1.2rem;
  }

  .hero-subtitle {
    font-size: 0.75rem;
  }

  .hero-description {
    font-size: 0.65rem;
  }
}

@media (max-width:980px) {
  .bg-curve {
    right: -8vw;
    bottom: -6vh;
    width: 120vw;
    height: 38vh;
    opacity: 0.85;
  }

  .hero-content { gap: 18px; }
  .hero-portrait { width: 320px; }
  .portrait-frame.big { width: 320px; height: 320px; padding: 16px; }
  .portrait-inner { width: 220px; height: 220px; }
  .hero-name-large { font-size: 3.2rem; }
}

/* -------------------------
   Corner mark: WEB / PROFILE
   ------------------------- */

.corner-mark {
  position: fixed;
  left: var(--corner-left);
  bottom: 24px;
  display: flex;
  align-items: flex-end;
  gap: 10px;
  z-index: 5; /* above curve and content */
  pointer-events: auto;
  user-select: none;
}

.vertical-web {
  display: flex;
  flex-direction: column;
  gap: 0;
  align-items: center;
  transform-origin: left bottom;
}

.vertical-web span {
  display: block;
  font-weight: 900;
  font-size: 4rem;
  line-height: 0.9;
  color: #ffffff;
  letter-spacing: 0.1em;
  transition: color .25s ease, text-shadow .25s ease;
  text-shadow: 0 6px 18px rgba(0,0,0,0.6);
}

.horizontal-profile {
  font-weight: 900;
  font-size: 3.8rem;
  color: #ffffff;
  white-space: nowrap;
  align-self: center;
  margin-left: -6px;
  transition: color .25s ease, text-shadow .25s ease, transform .25s ease;
  text-shadow: 0 6px 18px rgba(0,0,0,0.6);
}

/* animated color shift */
@keyframes colorShift {
  0%   { color: #ffffff; text-shadow: 0 6px 18px rgba(0,0,0,0.6); }
  25%  { color: var(--leaf); text-shadow: 0 10px 30px rgba(25,209,139,0.10); }
  50%  { color: #ffffff; text-shadow: 0 6px 18px rgba(0,0,0,0.6); }
  75%  { color: var(--leaf); text-shadow: 0 10px 30px rgba(25,209,139,0.10); }
  100% { color: #ffffff; text-shadow: 0 6px 18px rgba(0,0,0,0.6); }
}

@keyframes hoverPulse {
  0%   { color: var(--leaf-strong); text-shadow: 0 0 28px rgba(0,199,110,0.55); transform: translateY(-2px); }
  50%  { color: #ffffff; text-shadow: 0 0 10px rgba(255,255,255,0.12); transform: translateY(-6px); }
  100% { color: var(--leaf-strong); text-shadow: 0 0 28px rgba(0,199,110,0.55); transform: translateY(-2px); }
}

/* staggered animate letters */
.vertical-web span:nth-child(1) { animation: colorShift 3.2s linear infinite; animation-delay: 0s; }
.vertical-web span:nth-child(2) { animation: colorShift 3.2s linear infinite; animation-delay: .3s; }
.vertical-web span:nth-child(3) { animation: colorShift 3.2s linear infinite; animation-delay: .6s; }
.horizontal-profile { animation: colorShift 3.6s linear infinite; animation-delay: 0.9s; }

/* hover stronger pulse */
.corner-mark:hover .vertical-web span,
.corner-mark:hover .horizontal-profile {
  animation: hoverPulse 1.6s ease-in-out infinite;
  cursor: pointer;
}

/* responsive adjustments */
@media (max-width:980px) {
  .corner-mark { left: calc(var(--corner-left) + 6px); bottom: 12px; }
  .vertical-web span { font-size: 2.2rem; }
  .horizontal-profile { font-size: 2rem; margin-left: -4px; }
  .hero-name-large { font-size: 3rem; }
}
</style>
