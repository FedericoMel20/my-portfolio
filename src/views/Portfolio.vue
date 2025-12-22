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
          <span class="cta" role="button">Click to see Item</span>
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
          title: "Introduction To AI",
          subtitle: "Coursera - IBM",
          tags: ["Machine Learning Basics", "AI Fundamentals"],
          desc: "Gained a foundational understanding of artificial intelligence, including machine learning, deep learning, natural language processing, and real-world AI applications. Explored ethical considerations and the impact of AI across industries.",
          avatar: "../src/assets/intro_ai.jpeg",
          link: "https://coursera.org/share/207663c8ce855f51d7b5225d3493b003",
        },
        {
          id: 5,
          tab: "Certificates",
          type: "CERTIFICATE",
          title: "Python for Data Science, AI and Development",
          subtitle: "Coursera - IBM",
          tags: ["Python", "NumPY", "Pandas", "Data Science"],
          desc: "Learned Python fundamentals and applied them to data science and AI workflows, including data structures, control flow, functions, and libraries commonly used in analytics and machine learning.",
          avatar: "../src/assets/python_ai.jpeg",
          link: "https://coursera.org/share/c25a11e8455603f25fa2169b77571a3c",
        },
        {
          id: 6,
          tab: "Certificates",
          type: "CERTIFICATE",
          title: "Web Development",
          subtitle: "Sololearn",
          tags: ["HTML", "JavaScript", "CSS"],
          desc: "Learned the fundamentals of web development with a focus on HTML, CSS, and responsive design principles for building clean and functional websites.",
          avatar: "../src/assets/web_dev.jpeg",
          link: "https://www.sololearn.com/certificates/CC-EB5KFMAF",
        },
        {
          id: 7,
          tab: "Certificates",
          type: "CERTIFICATE",
          title: "Generative AI: Prompt Engineering Basics",
          subtitle: "IBM - Coursera",
          tags: ["Generative AI", "Prompt Engineering"],
          desc: "Learned the fundamentals of generative AI and f  ocused on crafting precise prompts to enhance accuracy, control, and reliability in generative AI systems.",
          avatar: "../src/assets/prompt_engineering.jpg",
          link: "https://coursera.org/share/0475a990a2554fa735cedffb741a6681",
        },
        {
          id: 8,
          tab: "Certificates",
          type: "CERTIFICATE",
          title: "Python Developer",
          subtitle: "Core Python Programming & Problem Solving",
          tags: ["Python", "Problem Solving", "OOP"],
          desc: "Developed a solid understanding of Python programming, including variables, control structures, functions, and practical problem-solving techniques through hands-on exercises.",
          avatar: "../src/assets/python_dev.png",
          link: "https://www.sololearn.com/certificates/CC-WKIANOOI",
        },
        {
          id: 9,
          tab: "Certificates",
          type: "CERTIFICATE",
          title: "Generative AI: Introduction and Applications",
          subtitle: "Generative Models and Practical Applications",
          tags: ["Deep Learning", "ChatGPT", "Prototyping"],
          desc: "Gained foundational knowledge of generative AI concepts, models, and real-world applications, including how generative systems create text, images, and data-driven outputs.",
          avatar: "../src/assets/gen_ai.jpeg",
          link: "https://coursera.org/share/290d1b8cffa71c8a52abc0856455e181",
        },
        {
          id: 10,
          tab: "Certificates",
          type: "CERTIFICATE",
          title: "Python Intermediate",
          subtitle: "Data Structures & Logic in Python",
          tags: ["Python", "Data Structures", "OOP"],
          desc: "Strengthened intermediate Python skills, focusing on data structures, functions, modules, and logical problem-solving through hands-on coding exercises.",
          avatar: "../src/assets/python_int.jpeg",
          link: "https://www.sololearn.com/certificates/CC-GU7G2K5S",
        },
        {
          id: 9,
          tab: "Certificates",
          type: "CERTIFICATE",
          title: "TOEFL iBT",
          subtitle: "International English Proficiency Assessment",
          tags: ["English", "Communication", "Academic Writing"],
          desc: "Certified academic English proficiency for global academic and professional contexts.",
          avatar: "../src/assets/toefl.jpeg",
          link: "https://drive.google.com/file/d/1FEc69s7rmeJyfVilBxAdWRCb1JjcOzEM/view?usp=sharing",
        },
        {
          id: 10,
          tab: "Projects",
          type: "PROJECT",
          title: "Loud Whispers",
          subtitle: "A Poetry Mobile App for Poem Lovers and Readers",
          tags: ["TypeScript", "React-Native", "Mobile App"],
          desc: "Loud Whispers is a mobile poetry application built and designed to provide a calm and immersive reading experience for poetry lovers. The app focuses on clean navigation, expressive typography, and a distraction-free interface to highlight written emotions and artistic expression.",
          avatar: "../src/assets/logo.jpg",
          link: "https://github.com/FedericoMel20/PoetryApp.git",
        },
        {
          id: 11,
          tab: "Projects",
          type: "PROJECT",
          title: "Web Portfolio",
          subtitle: "Interactive 3D Portfolio Website",
          tags: ["Vue.js", "CSS3D",],
          desc: "A highly interactive personal web portfolio built with Vue.js, featuring animated 3D interfaces, dynamic content transitions, and smooth user interactions. Immersive visual design and modern frontend techniques.",
          avatar: "../src/assets/web_portfolio.png",
          link: "https://github.com/FedericoMel20/my-portfolio.git",
        },
        {
          id: 12,
          tab: "Projects",
          type: "PROJECT",
          title: "OOP Projects",
          subtitle: "Python OOP Mini Projects Collection",
          tags: ["Python", "OOP", "Mini Projects"],
          desc: "A collection of problem-solving mini projects built using Python's Object-Oriented Programming paradigm, showcasing encapsulation, inheritance, and polymorphism concepts.",
          avatar: "../src/assets/OOP.png",
          link: "https://github.com/FedericoMel20/Object_Oriented_Programming.git",
        },
        {
          id: 13,
          tab: "Projects",
          type: "PROJECT",
          title: "Smart Farming System",
          subtitle: "GIS-Based Smart Farming System",
          tags: ["GIS", "HTML", "API"],
          desc: "A GIS-based smart farming system designed to support Gambian farmers by analyzing geospatial and environmental data to improve agricultural planning and decision-making. The project leverages geographic information systems to visualize land conditions, optimize resource usage, and promote sustainable farming practices. (Still in progress)",
          avatar: "../src/assets/homebg.png",
          link: "https://github.com/FedericoMel20/GIS.git",
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
/*
  Caption behavior:
  - Fade in approx. 2s after a card becomes active (enter uses 2s delay).
  - Fade out immediately when the card goes inactive.
  - Layout is two columns: left (type/title/subtitle/tags), right (description).
*/
.caption {  /* remove link underlines from caption content */
  text-decoration: none;  position: absolute;
  left: 50%;
  top: 70%;
  transform: translate(-50%, -55%); /* slightly up from center */
  width: min(600px, 82%);
  min-height: 72px; /* reduced vertical size */
  padding: 12px 18px 40px; /* bottom space for CTA */
  border-radius: 12px;

  background: linear-gradient(180deg, rgba(0,0,0,0.92), rgba(0,0,0,0.78));
  border: 1px solid rgba(255,255,255,0.06);
  backdrop-filter: blur(10px);

  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 12px 18px;
  color: #fff;
  z-index: 1300;
  align-items: start; 
}

/* Enter/leave transitions (Vue transition wrapper uses `caption` name) */
.caption-enter-active {
  transition: opacity .5s ease 0.5s, transform .5s cubic-bezier(.22,.9,.32,1) 2s;
}
.caption-leave-active {
  transition: opacity .22s ease 0s, transform .22s ease 0s;
}
.caption-enter-from { opacity: 0; transform: translate(-50%, -50%) translateY(8px) scale(.998); }
.caption-enter-to   { opacity: 1; transform: translate(-50%, -55%) translateY(0) scale(1); }
.caption-leave-to   { opacity: 0; transform: translate(-50%, -55%) translateY(8px) scale(.998); }

/* Left column (metadata) */
.caption-left {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  padding: 6px 10px;
  text-align: left;
  gap: 6px;
}

.caption .type {
  color: #19d18b; /* alive green */
  font-weight: 800;
  letter-spacing: 1.6px;
  font-size: 0.72rem;
  margin-bottom: 6px;
  text-transform: uppercase;
}

.caption h2 {
  font-size: 2rem; /* larger, commanding */
  margin: 0 0 6px 0;
  font-weight: 900;
  line-height: 1.02;
  /* primary title font - ensure 'Stinger Fit' is available locally or via webfont */
  font-family: 'Stinger Fit', 'Poppins', system-ui, -apple-system, 'Segoe UI', Roboto, 'Helvetica Neue', Arial;
  color: #ffffff;
  letter-spacing: -0.6px;
}


.caption .subtitle {
  font-size: 0.95rem;
  font-weight: 300; /* lighter modern feel */
  color: rgba(255,255,255,0.68);
  margin: 0 0 8px 0;
  font-family: 'Courier New', Courier, monospace; /* retro/techy feel */
}


.caption .tags {
  display:flex;
  gap:8px;
  flex-wrap:wrap;
  margin-top:8px;
}
.caption .tags span {
  background: transparent;
  padding: 4px 10px;
  border-radius: 999px;
  font-size: 0.78rem;
  font-weight: 600;
  color: #ffffff;
  border: 1px solid rgba(255,255,255,0.95);
  font-family: 'Segoe Fluent Icons', 'Segoe UI', system-ui, sans-serif;
  letter-spacing: 0.2px;
}

/* Right column (description) */
.caption-right { padding: 6px 8px; }
.caption .desc {
  font-size: 0.95rem;
  color: rgba(255,255,255,0.95);
  font-family: 'Work Sans', system-ui, -apple-system, 'Segoe UI', Roboto, 'Helvetica Neue', Arial;
  font-weight: 400;
  line-height: 1.36;
  margin: 0;
  text-align: left;
}

/* CTA bottom-right */
.caption .cta {
  position: absolute;
  right: 12px;
  bottom: 12px;
  color: #00ffb8;
  font-weight: 900;
  font-size: 0.98rem;
  padding: 6px 10px;
  border-radius: 8px;
  text-decoration: none;
  transition: transform .12s ease, box-shadow .18s ease, color .12s ease;
}
.caption:hover .cta { transform: translateY(-3px); box-shadow: 0 6px 26px rgba(0,255,170,0.25), 0 0 18px rgba(0,255,170,0.18); color: #ccfff2 }

/* Corner glows - kept from previous design */
.caption:hover {
  box-shadow: 0 14px 48px rgba(25,209,139,0.12);
  border-color: rgba(25,209,139,0.98);
}
.caption:hover::before {
  content: '';
  position: absolute;
  left: 8px;
  top: 8px;
  width: 80px;
  height: 80px;
  background: radial-gradient(circle at left top, rgba(25,209,139,0.98), rgba(25,209,139,0) 55%);
  border-radius: 12px;
}
.caption:hover::after {
  content: '';
  position: absolute;
  right: 8px;
  top: 8px;
  width: 80px;
  height: 80px;
  background: radial-gradient(circle at right top, rgba(25,209,139,0.98), rgba(25,209,139,0) 55%);
  border-radius: 12px;
}
.caption:hover .corner-bottom-left {
  content: '';
  position: absolute;
  left: 8px;
  bottom: 8px;
  width: 80px;
  height: 80px;
  background: radial-gradient(circle at left bottom, rgba(25,209,139,0.98), rgba(25,209,139,0) 55%);
  border-radius: 12px;
}
.caption:hover .corner-top-right {
  content: '';
  position: absolute;
  right: 8px;
  bottom: 8px;
  width: 80px;
  height: 80px;
  background: radial-gradient(circle at right bottom, rgba(25,209,139,0.98), rgba(25,209,139,0) 55%);
  border-radius: 12px;
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
