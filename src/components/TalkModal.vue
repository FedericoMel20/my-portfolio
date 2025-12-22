<template>
  <div class="modal-backdrop" @click.self="close" role="dialog" aria-modal="true" aria-label="Contact modal">
    <div class="modal-card">

      <h2 class="modal-title">Let's Talk</h2>
      <p class="modal-sub">I’d love to hear about your project — one step at a time.</p>

      <!-- Progress -->
      <div class="progress" aria-hidden="true">
        <span class="dot" :class="{active: step === 1}"></span>
        <span class="dot" :class="{active: step === 2}"></span>
      </div>

      <transition name="fade" mode="out-in">
        <div key="step-1" v-if="step === 1" class="step">
          <div class="form-field">
            <label for="name">Your name</label>
            <input id="name" ref="nameInput" v-model="name" type="text" placeholder="Enter your name (optional)" @keyup.enter="nextStep" maxlength="80" />
            <small class="hint muted">You can leave this blank if you prefer to stay anonymous.</small>
          </div>

          <div class="modal-actions">
            <button class="cancel-btn" @click="close">Cancel</button>
            <button class="send-btn" @click="nextStep">Next</button>
          </div>
        </div>

        <div key="step-2" v-else class="step">
          <div class="form-field">
            <label for="message">What do you have in mind?</label>
            <textarea id="message" ref="messageInput" v-model="message" placeholder="Briefly describe your idea or request — e.g. a website, feature, or collaboration" rows="5" @keydown.enter="onTextareaEnter"></textarea>
            <small class="hint muted">Tip: Press <kbd>Ctrl</kbd>+<kbd>Enter</kbd> (or ⌘+Enter on Mac) to send.</small>
          </div>

          <div v-if="error" class="error">{{ error }}</div>

          <div class="modal-actions">
            <button class="cancel-btn" @click="prevStep">Back</button>
            <button class="send-btn" :disabled="sending" @click="sendWhatsApp">Send</button>
          </div>
        </div>
      </transition>

    </div>
  </div>
</template>

<script>
export default {
  name: "TalkModal",
  emits: ["close"],

  data() {
    return {
      step: 1,
      name: "",
      message: "",
      phone: "628567219006",
      sending: false,
      error: "",
    }
  },

  mounted() {
    this.focusCurrent()
  },

  watch: {
    step() {
      this.$nextTick(() => this.focusCurrent())
    }
  },

  methods: {
    focusCurrent() {
      if (this.step === 1 && this.$refs.nameInput) this.$refs.nameInput.focus()
      if (this.step === 2 && this.$refs.messageInput) this.$refs.messageInput.focus()
    },

    close() {
      this.$emit("close")
    },

    nextStep() {
      this.error = ""
      this.step = 2
    },

    prevStep() {
      this.error = ""
      this.step = 1
    },

    onTextareaEnter(e) {
      // Only submit on Ctrl/Cmd + Enter; otherwise allow newline
      if (e.ctrlKey || e.metaKey) {
        e.preventDefault()
        this.sendWhatsApp()
      }
    },

    sendWhatsApp() {
      this.error = ""
      const n = this.name.trim() || "Someone"
      const m = this.message.trim()

      if (!m) {
        this.error = "Please tell me what you have in mind so I can help."
        return
      }

      this.sending = true

      // Construct a friendly, professional WhatsApp message
      const text = `Hi Mambuna, my name is ${n}.%0A%0AI'd like to discuss: ${m}`

      // Use wa.me link
      const url = `https://wa.me/${this.phone}?text=${text}`

      // Open WhatsApp in a new tab/window
      window.open(url, "_blank")

      // small delay for visual feedback
      setTimeout(() => {
        this.sending = false
        this.close()
      }, 350)
    }
  }
}
</script>

<style scoped>
/* Backdrop */
.modal-backdrop {
  position: fixed;
  inset: 0;
  background: rgba(0,0,0,0.55);
  backdrop-filter: blur(6px);
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 5000;
}

/* Modal Card */
.modal-card {
  width: 420px;
  background: var(--card);
  padding: 24px;
  border-radius: 14px;
  border: 1px solid var(--border);
  box-shadow: 0 0 34px rgba(25,209,139,0.15), 0 0 12px rgba(25,209,139,0.25);
  animation: popIn .35s ease;
}

@keyframes popIn {
  from { transform: scale(0.95); opacity: 0; }
  to   { transform: scale(1); opacity: 1; }
}

.modal-title {
  margin: 0;
  font-size: 1.6rem;
  color: var(--accent);
  font-weight: 800;
}

.modal-sub {
  margin-bottom: 12px;
  color: var(--muted);
}

.progress { display:flex; gap:8px; margin: 12px 0; }
.dot { width:8px; height:8px; background: rgba(255,255,255,0.06); border-radius:50%; transition: all .18s ease; }
.dot.active { background: var(--accent); box-shadow: 0 6px 18px rgba(25,209,139,0.18); transform: translateY(-2px); }

.fade-enter-active, .fade-leave-active { transition: opacity .18s, transform .18s; }
.fade-enter-from { opacity:0; transform: translateY(6px); }
.fade-enter-to { opacity:1; transform: translateY(0); }
.fade-leave-from { opacity:1; transform: translateY(0); }
.fade-leave-to { opacity:0; transform: translateY(6px); }

/* Form styling */
.form-field {
  display: flex;
  flex-direction: column;
  margin-bottom: 12px;
}

.form-field label {
  margin-bottom: 6px;
  font-weight: 700;
  color: var(--accent);
}

.form-field input,
.form-field textarea {
  padding: 12px;
  border-radius: 10px;
  background: rgba(255,255,255,0.03);
  border: 1px solid var(--border);
  color: white;
  outline: none;
}

.form-field .hint { margin-top:6px; font-size:0.82rem; color:var(--muted); }

kbd { background: rgba(255,255,255,0.04); padding: 2px 6px; border-radius: 6px; font-weight:700; color:var(--muted); }

.error { color: #ffb4b4; background: rgba(255,80,80,0.06); padding:8px 10px; border-radius:8px; margin-top:6px; font-weight:700; }

/* Actions */
.modal-actions { display:flex; justify-content:space-between; margin-top: 14px; }

.cancel-btn, .send-btn { padding: 10px 16px; border-radius: 10px; cursor:pointer; border:none; font-weight:700; }
.cancel-btn { background: rgba(255,255,255,0.08); color:var(--muted); }
.cancel-btn:hover { background: rgba(255,255,255,0.12); }
.send-btn { background: var(--accent); color: #001; box-shadow: 0 0 16px rgba(25,209,139,0.35); }
.send-btn[disabled] { opacity:0.6; cursor:not-allowed; filter:grayscale(0.05); }

/* Responsive */
@media (max-width:520px) {
  .modal-card { width: 92%; padding:18px; }
}
</style>
