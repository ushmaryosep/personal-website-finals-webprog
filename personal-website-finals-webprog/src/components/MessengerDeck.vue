<template>
  <div class="messenger-screen">
    <div class="content-wrapper">
      <h1 class="messenger-title">🕊️ CAPTAIN'S LEDGER</h1>
      <p class="messenger-subtitle">Leave your mark on the Grand Line.</p>

      <div class="layout-grid">
        <div class="input-section">
          <h3 class="section-label">LOG A MESSAGE</h3>
          <form @submit.prevent="sendMessage" class="ledger-form">
            <input v-model="messengerName" type="text" placeholder="Name / Crew" required />
            <textarea v-model="messageContent" placeholder="Your message..." required></textarea>
            <button type="submit" :disabled="isSending" class="submit-btn">
              {{ isSending ? 'SENDING...' : 'LOG MESSAGE ⚓' }}
            </button>
          </form>
          <p v-if="statusMsg" class="status-text">{{ statusMsg }}</p>

          <div class="social-links-area">
            <h3 class="section-label">DEN DEN MUSHI</h3>
            <div class="social-btns">
              <a href="https://www.facebook.com/joshmar.clavero" target="_blank" class="social-icon">
                <img src="https://cdn-icons-png.flaticon.com/512/733/733547.png" alt="FB" />
              </a>
              <a href="https://www.instagram.com/ushmaryosep/" target="_blank" class="social-icon">
                <img src="https://cdn-icons-png.flaticon.com/512/2111/2111463.png" alt="IG" />
              </a>
              <a href="https://www.linkedin.com/in/joshmar-clavero-8b1912322/" target="_blank" class="social-icon">
                <img src="https://cdn-icons-png.flaticon.com/512/145/145807.png" alt="LI" />
              </a>
              <a href="https://github.com/ushmaryosep" target="_blank" class="social-icon">
                <img src="https://cdn-icons-png.flaticon.com/512/733/733553.png" alt="GH" />
              </a>
              <a href="mailto:jmclavero25@gmail.com" class="social-icon">
                <img src="https://cdn-icons-png.flaticon.com/512/732/732200.png" alt="Mail" />
              </a>
            </div>
          </div>
        </div>

        <div class="comments-section">
          <h3 class="section-label">RECENT LOGS</h3>
          <div class="message-list">
            <div v-if="fetching" class="loading-logs">Reading scrolls...</div>
            <div v-for="msg in messages" :key="msg.id" class="message-item">
              <span class="msg-author">{{ msg.messenger_name }}</span>
              <p class="msg-text">{{ msg.message_content }}</p>
            </div>
          </div>
        </div>
      </div>

      <button @click="$emit('close')" class="back-to-deck-btn">← RETURN TO DECK</button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      messengerName: '',
      messageContent: '',
      isSending: false,
      fetching: true,
      statusMsg: '',
      messages: [],
      supabaseUrl: 'https://obexkjwpjkqqiozdaezv.supabase.co', 
      supabaseAnonKey: 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6Im9iZXhrandwamtxcWlvemRhZXp2Iiwicm9sZSI6ImFub24iLCJpYXQiOjE3NzE4NjYwMjgsImV4cCI6MjA4NzQ0MjAyOH0.daEcBIw4qHEQXTMA7yU0JMS2g5kjLEceEpiiYutZdRk'
    }
  },
  mounted() {
    this.fetchMessages();
  },
  methods: {
    async fetchMessages() {
      try {
        const response = await fetch(`${this.supabaseUrl}/rest/v1/messages?select=*&order=created_at.desc&limit=12`, {
          headers: {
            'apikey': this.supabaseAnonKey,
            'Authorization': `Bearer ${this.supabaseAnonKey}`
          }
        });
        this.messages = await response.json();
      } finally {
        this.fetching = false;
      }
    },
    async sendMessage() {
      this.isSending = true;
      try {
        const response = await fetch(`${this.supabaseUrl}/rest/v1/messages`, {
          method: 'POST',
          headers: {
            'apikey': this.supabaseAnonKey,
            'Authorization': `Bearer ${this.supabaseAnonKey}`,
            'Content-Type': 'application/json',
            'Prefer': 'return=minimal'
          },
          body: JSON.stringify({
            messenger_name: this.messengerName,
            message_content: this.messageContent
          })
        });

        if (response.ok) {
          this.statusMsg = "SUCCESS!";
          this.messengerName = '';
          this.messageContent = '';
          this.fetchMessages();
        }
      } catch (error) {
        this.statusMsg = "FAILED!";
      } finally {
        this.isSending = false;
      }
    }
  }
}
</script>

<style scoped>
/* 1. MAIN SCREEN SETUP */
.messenger-screen {
  position: absolute; top: 0; left: 0; width: 100vw; height: 100vh;
  display: flex; justify-content: flex-start; align-items: center; 
  padding: 0 4%;
  background: linear-gradient(to right, rgba(0,0,0,0.85) 25%, rgba(0,0,0,0.1) 100%), 
              url('https://github.com/ushmaryosep/personal-website-finals-webprog/blob/main/assets(gif%2C%20png%2C%20jpg)/final%20bg.gif') no-repeat center center;
  background-size: cover;
  z-index: 70;
}

.content-wrapper {
  width: 100%; max-width: 420px;
  height: 85vh;
  display: flex;
  flex-direction: column;
}

/* 2. TEXT & HEADERS */
.messenger-title { font-family: 'Bangers'; color: #f4d03f; font-size: 1.8rem; letter-spacing: 1px; }
.messenger-subtitle { color: #aaa; font-size: 0.8rem; margin-bottom: 25px; font-family: 'Oswald'; }
.section-label { font-family: 'Bangers'; color: #f4d03f; font-size: 1rem; margin-bottom: 10px; opacity: 0.8; }

/* 3. THE INVISIBLE SCROLLBAR ENGINE */
.layout-grid {
  display: flex;
  flex-direction: column;
  gap: 20px;
  overflow-y: scroll; /* Allow scrolling */
  padding-right: 5px;
  
  /* Hide scrollbar for Chrome, Safari and Opera */
  &::-webkit-scrollbar {
    display: none;
  }
  /* Hide scrollbar for IE, Edge and Firefox */
  -ms-overflow-style: none;  /* IE and Edge */
  scrollbar-width: none;  /* Firefox */
}

/* 4. FORM & INPUTS */
.ledger-form { display: flex; flex-direction: column; gap: 12px; }
.ledger-form input, .ledger-form textarea {
  background: rgba(255,255,255,0.05); border: none; border-bottom: 1px solid #333; 
  color: white; padding: 8px; font-family: 'Oswald'; font-size: 0.85rem; outline: none;
}
.ledger-form input:focus, .ledger-form textarea:focus { border-bottom-color: #f4d03f; background: rgba(255,255,255,0.08); }
.ledger-form textarea { height: 60px; resize: none; }

.submit-btn {
  background: #f4d03f; color: black; border: none; padding: 8px;
  font-family: 'Bangers'; font-size: 1rem; cursor: pointer; transition: 0.2s;
}
.submit-btn:hover { background: white; transform: scale(1.02); }

/* 5. SOCIAL LOGOS */
.social-links-area { margin-top: 15px; }
.social-btns { display: flex; gap: 18px; }
.social-icon img {
  width: 20px; height: 20px; filter: invert(1) brightness(0.8); transition: 0.3s;
}
.social-icon:hover img { filter: invert(82%) sepia(54%) saturate(464%) hue-rotate(351deg) brightness(101%) contrast(92%); transform: translateY(-3px); }

/* 6. MESSAGE LIST */
.message-list { display: flex; flex-direction: column; gap: 12px; }
.message-item {
  padding: 8px 0; border-bottom: 1px solid rgba(255, 255, 255, 0.05);
}
.msg-author { color: #f4d03f; font-weight: bold; font-size: 0.8rem; font-family: 'Bangers'; letter-spacing: 0.5px; }
.msg-text { font-size: 0.8rem; color: #bbb; font-family: 'Oswald'; margin-top: 2px; line-height: 1.4; }

/* 7. RETURN BUTTON */
.back-to-deck-btn {
  margin-top: 20px; background: none; border: 1px solid rgba(255,255,255,0.2); color: #888;
  padding: 6px 15px; cursor: pointer; font-family: 'Oswald'; font-size: 0.75rem; width: fit-content; transition: 0.3s;
}
.back-to-deck-btn:hover { border-color: #f4d03f; color: #f4d03f; background: rgba(244, 208, 63, 0.05); }

.loading-logs { font-family: 'Oswald'; font-size: 0.8rem; color: #666; font-style: italic; }
</style>