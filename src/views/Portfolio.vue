<template>
  <main class="portfolio-view">

    <!-- SUB TABS -->
    <div class="portfolio-subtabs">
      <button
        v-for="t in tabs"
        :key="t"
        :class="['subtab', { active: activeTab === t }]"
        @click="setTab(t)"
      >
        {{ t }}
      </button>
    </div>

    <!-- ORBIT STAGE -->
    <section
      class="orbit-stage"
      @mousemove="onMouseMove"
      @mouseleave="resetTilt"
      @mousedown="startDrag"
      @mousemove.stop="onDrag"
      @mouseup="endDrag"
      @mouseleave.stop="endDrag"
      @touchstart="startDrag"
      @touchmove="onDrag"
      @touchend="endDrag"
    >
      <!-- LEFT ARROW -->
      <button class="nav-arrow left" @click="prev">‹</button>

      <!-- ORBIT -->
      <div class="orbit" ref="orbit">
        <div
          v-for="(item, i) in filteredItems"
          :key="item.id"
          class="orbit-avatar"
          :class="{ active: i === activeIndex }"
          :style="avatarStyle(i)"
        >
          <img :src="item.avatar" :alt="item.title" />
        </div>
      </div>

      <!-- RIGHT ARROW -->
      <button class="nav-arrow right" @click="next">›</button>
    </section>

    <!-- CAPTION -->
    <transition name="caption" mode="out-in">
      <a
        v-if="activeItem"
        :key="activeItem.id"
        class="caption"
        :href="activeItem.link"
        target="_blank"
        rel="noopener noreferrer"
      >
        <div class="caption-left">
          <span class="type">{{ activeItem.type }}</span>
          <h2>{{ activeItem.title }}</h2>
          <p class="subtitle">{{ activeItem.subtitle }}</p>

          <div class="tags">
            <span v-for="t in activeItem.tags" :key="t">{{ t }}</span>
          </div>
        </div>

        <div class="caption-right">
          <p class="desc">{{ activeItem.desc }}</p>
          <span class="cta">View details →</span>
        </div>
      </a>
    </transition>

  </main>
</template>

<script>
export default {
  name: "Portfolio",

  data() {
    return {
      tabs: ["Certificates", "Experience", "Projects"],
      activeTab: "Experience",
      activeIndex: 0,

      // tilt
      tiltX: 0,
      tiltY: 0,

      // drag / inertia
      dragging: false,
      startX: 0,
      velocity: 0,
      inertiaRAF: null,

      items: [
        {
          id: 1,
          tab: "Experience",
          type: "EXPERIENCE",
          title: "ANGGOTA HMTI",
          subtitle: "Himpunan Mahasiswa Teknik Informatika",
          tags: ["Organization", "Teamwork"],
          desc: "Aktif dalam kegiatan organisasi dan pengembangan komunitas TI.",
          avatar: "/avatars/exp1.png",
          link: "#",
        },
        {
          id: 2,
          tab: "Experience",
          type: "EXPERIENCE",
          title: "MAGANG AKTIF PROGRESIF",
          subtitle: "DPM Nusa Putra — Divisi 4",
          tags: ["Management", "Coordination"],
          desc: "Koordinasi program kampus dan dokumentasi kebijakan internal.",
          avatar: "/avatars/exp2.png",
          link: "#",
        },
        {
          id: 3,
          tab: "Experience",
          type: "EXPERIENCE",
          title: "FREELANCE PROJECTS",
          subtitle: "Self-Employed",
          tags: ["Web", "Problem Solving"],
          desc: "Pengembangan aplikasi web dan eksplorasi teknologi baru.",
          avatar: "/avatars/exp3.png",
          link: "#",
        },
        {
          id: 4,
          tab: "Certificates",
          type: "CERTIFICATE",
          title: "Introduction to AI",
          subtitle: "Coursera - IBM",
          tags: ["Web", "Problem Solving"],
          desc: "Pengembangan aplikasi web dan eksplorasi teknologi baru.",
          avatar: "../src/assets/intro_ai.jpeg",
          link: "#",
        },
        {
          id: 5,
          tab: "Certificates",
          type: "CERTIFICATE",
          title: "Python for Data Science, AI and Development",
          subtitle: "Coursera - IBM",
          tags: ["Web", "Problem Solving"],
          desc: "Pengembangan aplikasi web dan eksplorasi teknologi baru.",
          avatar: "../src/assets/python_ai.jpeg",
          link: "#",
        },
        {
          id: 6,
          tab: "Certificates",
          type: "CERTIFICATE",
          title: "Web Development",
          subtitle: "Sololearn - IBM",
          tags: ["Web", "Problem Solving"],
          desc: "Pengembangan aplikasi web dan eksplorasi teknologi baru.",
          avatar: "../src/assets/web_dev.jpeg",
          link: "#",
        },
        {
          id: 7,
          tab: "Certificates",
          type: "CERTIFICATE",
          title: "Generative AI: Prompt Engineering Basics",
          subtitle: "Sololearn - IBM",
          tags: ["Web", "Problem Solving"],
          desc: "Pengembangan aplikasi web dan eksplorasi teknologi baru.",
          avatar: "../src/assets/prompt_engineering.jpg",
          link: "#",
        },

      ],
    };
  },

  computed: {
    filteredItems() {
      return this.items.filter(i => i.tab === this.activeTab);
    },
    activeItem() {
      return this.filteredItems[this.activeIndex];
    },
  },

  methods: {
    setTab(tab) {
      this.activeTab = tab;
      this.activeIndex = 0;
    },

    avatarStyle(index) {
      const len = this.filteredItems.length;
      let offset = index - this.activeIndex;

      if (offset > len / 2) offset -= len;
      if (offset < -len / 2) offset += len;

      const angleStep = 32;           // angular spacing
      const radius = 520;             // reduced orbit radius so side cards sit closer behind
      const abs = Math.abs(offset);
      const isActive = abs === 0;

      // make side cards visible but faded
      const opacityMap = abs === 0 ? 1 : abs === 1 ? 0.85 : abs === 2 ? 0.55 : abs === 3 ? 0.28 : 0;

      return {
        transform: `
          rotateY(${offset * angleStep}deg)
          translateZ(${radius}px)
          translateY(${abs * 8}px)
          scale(${isActive ? 1.12 : 0.92})
        `,
        filter: isActive
          ? "grayscale(0%)"
          : "grayscale(100%) brightness(0.6)",
        opacity: opacityMap,
        zIndex: isActive ? 800 : 200 - abs * 10,
      };    
    },

    next() {
      this.activeIndex =
        (this.activeIndex + 1) % this.filteredItems.length;
    },

    prev() {
      this.activeIndex =
        (this.activeIndex - 1 + this.filteredItems.length) %
        this.filteredItems.length;
    },

    /* ===== MOUSE TILT ===== */
    onMouseMove(e) {
      const x = (e.clientX / window.innerWidth - 0.5) * 8;
      const y = (e.clientY / window.innerHeight - 0.5) * -6;

      this.$refs.orbit.style.transform =
        `translateX(-50%) rotateX(${y}deg) rotateY(${x}deg)`;
    },

    resetTilt() {
      this.$refs.orbit.style.transform =
        `translateX(-50%) rotateX(0deg) rotateY(0deg)`;
    },

    /* ===== DRAG + INERTIA ===== */
    startDrag(e) {
      this.dragging = true;
      this.startX = e.touches ? e.touches[0].clientX : e.clientX;
      this.velocity = 0;
      cancelAnimationFrame(this.inertiaRAF);
    },

    onDrag(e) {
      if (!this.dragging) return;
      const x = e.touches ? e.touches[0].clientX : e.clientX;
      const delta = x - this.startX;

      if (Math.abs(delta) > 40) {
        delta > 0 ? this.prev() : this.next();
        this.velocity = delta;
        this.startX = x;
      }
    },

    endDrag() {
      if (!this.dragging) return;
      this.dragging = false;

      const decay = () => {
        this.velocity *= 0.9;
        if (Math.abs(this.velocity) > 5) {
          this.velocity > 0 ? this.prev() : this.next();
          this.inertiaRAF = requestAnimationFrame(decay);
        }
      };
      this.inertiaRAF = requestAnimationFrame(decay);
    },
  },
};
</script>

<style scoped>
/* ================= BASE ================= */
.portfolio-view {
  height: 100vh;
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  justify-content: flex-start;
  padding-top: 6vh;
  overflow: hidden;
  position: relative;
} 

/* ================= SUBTABS ================= */
.portfolio-subtabs {
  position: absolute;
  top: 2.6vh;
  left: 50%;
  transform: translateX(-50%);
  display: flex;
  gap: 14px;
  z-index: 1200;
  padding: 6px 8px;
  background: rgba(0,0,0,0.14);
  border-radius: 999px;
  box-shadow: 0 12px 30px rgba(0,0,0,0.45);
}

.portfolio-subtabs .subtab {
  background: transparent;
  border: 1px solid rgba(255,255,255,0.06);
  color: rgba(255,255,255,0.9);
  padding: 8px 14px;
  border-radius: 999px;
  cursor: pointer;
  transition: box-shadow .2s ease, transform .12s ease, color .12s ease;
  font-weight: 600;
  letter-spacing: 0.6px;
}

.portfolio-subtabs .subtab:hover {
  box-shadow: 0 0 18px rgba(255,255,255,0.95);
  color: #fff;
  transform: translateY(-2px);
}

.portfolio-subtabs .subtab.active {
  background: linear-gradient(90deg, rgba(25,209,139,0.12), rgba(0,0,0,0));
  border-color: rgba(25,209,139,0.5);
  box-shadow: 0 8px 28px rgba(25,209,139,0.12);
  color: var(--accent);
} 

/* ================= ORBIT ================= */
.orbit-stage {
  position: relative;
  width: 100%;
  height: 60vh;
  perspective: 1600px;
  overflow: visible;
} 

.orbit {
  position: absolute;
  left: 44%; /* shifted slightly left */
  top: 18%;
  transform: translateX(-50%);  
  transform-style: preserve-3d;
  transition: transform .18s cubic-bezier(.22,.9,.32,1);
  will-change: transform;
} 
/* ================= AVATARS ================= */
.orbit-avatar {
  position: absolute;
  transform-style: preserve-3d;
  backface-visibility: hidden;
  transform-origin: center center;
  transition: transform .6s cubic-bezier(.22,.9,.32,1),
              filter .4s,
              opacity .4s;
} 

.orbit-avatar img {
  width: 200px;
  height: 200px;
  border-radius: 16px;
  object-fit: cover;
  box-shadow: 0 40px 140px rgba(0,0,0,0.75);
  transition: transform .28s cubic-bezier(.22,.9,.32,1), box-shadow .28s ease, filter .2s ease, opacity .3s ease;
  will-change: transform, filter, opacity;
  opacity: 0.9;
}

.orbit-avatar:not(.active) img {
  filter: grayscale(100%) brightness(0.65);
}

.orbit-avatar.active img {
  transform: scale(1.12);
  box-shadow: 0 80px 260px rgba(0,0,0,0.9), 0 0 36px 8px rgba(25,209,139,0.14);
  outline: 3px solid rgba(25,209,139,0.08);
  filter: none;
}


/* ================= CAPTION ================= */
.caption {
  margin-top: 28px;
  width: min(900px, 92%);
  padding: 14px 22px;
  border-radius: 16px;
  background: linear-gradient(180deg, rgba(0,0,0,0.86), rgba(0,0,0,0.72));
  border: 1px solid rgba(255,255,255,0.06);
  backdrop-filter: blur(10px);
  display: grid;
  grid-template-columns: 1fr 0.9fr;
  gap: 18px;
  text-decoration: none;
  color: #fff;
  z-index: 999;
  align-items: center;
} 

.caption h2 {
  font-size: 1.6rem;
  margin: 4px 0;
}

.caption .cta {
  color: var(--accent);
  font-weight: 700;
  margin-top: 10px;
  display: inline-block;
  font-size: 0.95rem;
} 

/* ================= ARROWS ================= */
.nav-arrow {
  position: absolute;
  top: 50%;
  width: 56px;
  height: 56px;
  border-radius: 50%;
  background: rgba(255,255,255,0.04);
  border: 1px solid rgba(255,255,255,0.08);
  color: #fff;
  font-size: 1.6rem;
  cursor: pointer;
  transition: background .18s ease, color .18s ease, filter .18s ease;
  z-index: 1400;
  pointer-events: auto;
}

.nav-arrow:hover {
  background: rgba(200,200,200,0.18);
  color: #222;
  filter: grayscale(40%);
}

.nav-arrow.left { left: 40px; }
.nav-arrow.right { right: 40px; }
</style>
