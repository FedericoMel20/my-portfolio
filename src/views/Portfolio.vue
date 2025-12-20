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
    <section class="orbit-stage">

      <!-- LEFT ARROW -->
      <button class="nav-arrow left" @click="prev">‹</button>

      <!-- ORBIT -->
      <div class="orbit">
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

    <!-- CAPTION (STABLE LAYER) -->
    <transition name="caption" mode="out-in">
      <a
        v-if="activeItem"
        :key="activeItem.id"
        class="caption"
        :href="activeItem.link"
        target="_blank"
        rel="noopener noreferrer"
      >
        <span class="type">{{ activeItem.type }}</span>
        <h2>{{ activeItem.title }}</h2>
        <p class="subtitle">{{ activeItem.subtitle }}</p>

        <div class="tags">
          <span v-for="t in activeItem.tags" :key="t">{{ t }}</span>
        </div>

        <p class="desc">{{ activeItem.desc }}</p>
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
      direction: 1, // 1 = forward, -1 = backward

      items: [
        /* ================= EXPERIENCE ================= */
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

        /* ================= PROJECTS ================= */
        {
          id: 4,
          tab: "Projects",
          type: "PROJECT",
          title: "Web Portfolio",
          subtitle: "Vue.js Interactive Site",
          tags: ["Vue", "Animation"],
          desc: "Portfolio modern dengan animasi sinematik.",
          avatar: "/avatars/proj1.png",
          link: "#",
        },
        {
          id: 5,
          tab: "Projects",
          type: "PROJECT",
          title: "Todo App",
          subtitle: "Full Stack App",
          tags: ["Node.js", "Vue"],
          desc: "Aplikasi manajemen tugas berbasis web.",
          avatar: "/avatars/proj2.png",
          link: "#",
        },
        {
          id: 6,
          tab: "Projects",
          type: "PROJECT",
          title: "Network Simulator",
          subtitle: "Packet Tracer",
          tags: ["Networking", "Simulation"],
          desc: "Simulasi jaringan komputer skala kecil.",
          avatar: "/avatars/proj3.png",
          link: "#",
        },

        /* ================= CERTIFICATES ================= */
        {
          id: 7,
          tab: "Certificates",
          type: "CERTIFICATE",
          title: "Web Development",
          subtitle: "Online Course",
          tags: ["HTML", "CSS", "JS"],
          desc: "Sertifikasi dasar pengembangan web.",
          avatar: "/avatars/cert1.png",
          link: "#",
        },
        {
          id: 8,
          tab: "Certificates",
          type: "CERTIFICATE",
          title: "Generative AI: Prompt Engineering Basics",
          subtitle: "IBM on Coursera",
          tags: ["AI", "Prompt Engineering"], 
          desc: "Dasar-dasar jaringan komputer.",
          avatar: "../src/assets/prompt_engineering.jpg",
          link: "https://coursera.org/share/0475a990a2554fa735cedffb741a6681",
        },
        {
          id: 9,
          tab: "Certificates",
          type: "CERTIFICATE",
          title: "Python for Data Science, AI & Development",
          subtitle: "IBM on Coursera",
          tags: ["Data Science", "Python", "AI"],
          desc: "Exploring the mathematical concepts and foundations of python in data science, AI, and machine learning.",
          avatar: "../src/assets/python_ai.jpeg",
          link: "https://coursera.org/share/c25a11e8455603f25fa2169b77571a3c",
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
      let offset = (index - this.activeIndex) * this.direction;

      if (offset > len / 2) offset -= len;
      if (offset < -len / 2) offset += len;

      const abs = Math.abs(offset);

      return {
        transform: `translateX(${offset * 360}px) translateY(${abs === 0 ? -20 : abs * 14}px) translateZ(${220 - abs * 130}px) scale(${abs === 0 ? 1.05 : 0.8})`,
        zIndex: abs === 0 ? 30 : 20 - abs,
        filter: abs === 0
          ? 'grayscale(0%)'
          : 'grayscale(100%) brightness(0.75)',
        opacity: abs > 4 ? 0 : 1,
      };
    },

    next() {
      this.direction = 1;
      this.activeIndex =
        (this.activeIndex + 1) % this.filteredItems.length;
    },

    prev() {
      this.direction = -1;
      this.activeIndex =
        (this.activeIndex - 1 + this.filteredItems.length) %
        this.filteredItems.length;
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
  align-items: center;
  justify-content: center;
  overflow: hidden;
}

/* ================= SUBTABS ================= */
.portfolio-subtabs {
  display: flex;
  gap: 18px;
  margin-bottom: 18px;
}

.subtab {
  padding: 8px 22px;
  border-radius: 999px;
  background: transparent;
  border: 1px solid rgba(255,255,255,0.08);
  color: var(--muted);
  font-weight: 700;
  cursor: pointer;
}

.subtab.active {
  color: var(--accent);
  background: rgba(25,209,139,0.18);
  box-shadow: 0 0 24px rgba(25,209,139,0.45);
}

/* ================= ORBIT ================= */
.orbit-stage {
  position: relative;
  width: 100%;
  height: 60vh;
  perspective: 1600px;
  display: flex;
  align-items: center;
  justify-content: center;
}

.orbit {
  position: relative;
  width: 100%;
  height: 100%;
  transform-style: preserve-3d;
}

/* ================= AVATARS ================= */
.orbit-avatar {
  position: absolute;
  left: 50%;
  top: 45%;               /* moved up slightly */
  transform-style: preserve-3d;
  transition: transform .8s cubic-bezier(.22,.9,.32,1),
              filter .6s,
              opacity .6s;
  z-index: 10;            /* below caption */
}

.orbit-avatar img {
  width: 240px;
  height: 240px;
  border-radius: 26px;
  object-fit: cover;
  box-shadow: 0 40px 140px rgba(0,0,0,0.7);
}

/* ================= CAPTION ================= */
.caption {
  position: relative;
  z-index: 50;            /* ALWAYS above avatars */
  margin-top: 40px;       /* extra breathing space */
  width: 680px;
  padding: 26px;
  border-radius: 18px;
  background: rgba(0,0,0,0.85);
  border: 1px solid rgba(25,209,139,0.35);
  text-decoration: none;
  color: #fff;
  transition: transform .3s;
} 

.caption:hover {
  transform: translateY(-6px);
  box-shadow: 0 0 50px rgba(25,209,139,0.45);
}

.type { color: var(--accent); font-size: .85rem; }
.subtitle, .desc { color: var(--muted); }

.tags {
  display: flex;
  gap: 10px;
  margin: 12px 0;
}

.tags span {
  padding: 6px 14px;
  border-radius: 999px;
  background: rgba(255,255,255,0.06);
}

/* ================= ARROWS ================= */
.nav-arrow {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  width: 56px;
  height: 56px;
  border-radius: 50%;
  background: rgba(255,255,255,0.04);
  border: 1px solid rgba(255,255,255,0.08);
  color: #fff;
  font-size: 1.6rem;
  cursor: pointer;
}

.nav-arrow.left { left: 40px; }
.nav-arrow.right { right: 40px; }

/* ================= CAPTION ANIM ================= */
.caption-enter-active,
.caption-leave-active {
  transition: all .4s ease;
}

.caption-enter-from {
  opacity: 0;
  transform: translateY(16px);
}

.caption-leave-to {
  opacity: 0;
  transform: translateY(-16px);
}
</style>
