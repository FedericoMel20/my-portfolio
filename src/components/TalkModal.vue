<template>
  <div class="modal-backdrop" @click.self="close">
    <div class="modal-card">

      <h2 class="modal-title">Let's Talk</h2>
      <p class="modal-sub">Fill in your details below</p>

      <div class="form-field">
        <label>Your Name</label>
        <input v-model="name" type="text" placeholder="Enter your name" />
      </div>

      <div class="form-field">
        <label>What do you have for me?</label>
        <textarea v-model="message" placeholder="Type your message..." rows="4"></textarea>
      </div>

      <div class="modal-actions">
        <button class="cancel-btn" @click="close">Cancel</button>
        <button class="send-btn" @click="sendWhatsApp">Send</button>
      </div>

    </div>
  </div>
</template>

<script>
export default {
  name: "TalkModal",
  emits: ["close"],

  data() {
    return {
      name: "",
      message: "",
      phone: "628567219006",
    }
  },

  methods: {
    close() {
      this.$emit("close")
    },

    sendWhatsApp() {
      const n = this.name.trim() || "Someone"
      const m = this.message.trim() || "Hello, I'd like to talk to you."

      // Construct WhatsApp message
      const text = `Name: ${n}\nMessage: ${m}`

      // WhatsApp API link
      const url = `https://wa.me/${this.phone}?text=${encodeURIComponent(text)}`

      window.open(url, "_blank")
      this.close()
    },
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
  width: 380px;
  background: var(--card);
  padding: 24px;
  border-radius: 14px;
  border: 1px solid var(--border);
  box-shadow: 0 0 34px rgba(25,209,139,0.15), 0 0 12px rgba(25,209,139,0.25);
  animation: popIn .35s ease;
}

@keyframes popIn {
  from { transform: scale(0.85); opacity: 0; }
  to   { transform: scale(1); opacity: 1; }
}

.modal-title {
  margin: 0;
  font-size: 1.6rem;
  color: var(--accent);
  font-weight: 800;
}

.modal-sub {
  margin-bottom: 18px;
  color: var(--muted);
}

/* Form styling */
.form-field {
  display: flex;
  flex-direction: column;
  margin-bottom: 14px;
}

.form-field label {
  margin-bottom: 6px;
  font-weight: 700;
  color: var(--accent);
}

.form-field input,
.form-field textarea {
  padding: 10px;
  border-radius: 10px;
  background: rgba(255,255,255,0.05);
  border: 1px solid var(--border);
  color: white;
}

/* Actions */
.modal-actions {
  display: flex;
  justify-content: space-between;
  margin-top: 14px;
}

/* Cancel Button */
.cancel-btn,
.send-btn {
  padding: 10px 16px;
  border-radius: 10px;
  cursor: pointer;
  border: none;
  font-weight: 700;
}

.cancel-btn {
  background: rgba(255,255,255,0.08);
  color: var(--muted);
}

.cancel-btn:hover {
  background: rgba(255,255,255,0.12);
}

/* Send button */
.send-btn {
  background: var(--accent);
  color: #001;
  box-shadow: 0 0 16px rgba(25,209,139,0.35);
}

.send-btn:hover {
  background: #00ffa3;
  box-shadow: 0 0 26px rgba(25,209,139,0.55);
}
</style>
