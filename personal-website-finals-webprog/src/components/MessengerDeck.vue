<template>
  <div class="messenger-screen">
    <div class="content-wrapper">
      <h1 class="messenger-title">🕊️ CAPTAIN'S LEDGER</h1>
      <p class="messenger-subtitle">Leave your mark on the Grand Line.</p>

      <div class="layout-grid">
        <div class="input-section">
          <div class="ledger-card">
            <h3>LOG A MESSAGE</h3>
            <form @submit.prevent="sendMessage" class="ledger-form">
              <input v-model="messengerName" type="text" placeholder="Name / Crew" required />
              <textarea v-model="messageContent" placeholder="Your message..." required></textarea>
              <button type="submit" :disabled="isSending">
                {{ isSending ? 'SENDING...' : 'LOG MESSAGE ⚓' }}
              </button>
            </form>
            <p v-if="statusMsg" class="status-text">{{ statusMsg }}</p>
          </div>

          <div class="social-links-card">
            <h3>DEN DEN MUSHI</h3>
            <div class="social-btns">
              <a href="https://www.facebook.com/joshmar.clavero" target="_blank" class="social-link">FB</a>
              <a href="https://www.instagram.com/ushmaryosep/" target="_blank" class="social-link">IG</a>
              <a href="https://www.linkedin.com/in/joshmar-clavero-8b1912322/" target="_blank" class="social-link">LI</a>
              <a href="https://github.com/ushmaryosep" target="_blank" class="social-link">GH</a>
            </div>
          </div>
        </div>

        <div class="comments-section">
          <h3>RECENT LOGS</h3>
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
        const response = await fetch(`${this.supabaseUrl}/rest/v1/messages?select=*&order=created_at.desc&limit=10`, {
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
          this.statusMsg = "LOGGED!";
          this.messengerName = '';
          this.messageContent = '';
          this.fetchMessages(); // Refresh list
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
.messenger-screen {
  position: absolute; top: 0; left: 0; width: 100vw; height: 100vh;
  display: flex; justify-content: flex-start; align-items: center; 
  padding: 0 5%;
  /* Background with a dimming overlay */
  background: linear-gradient(rgba(0,0,0,0.5), rgba(0,0,0,0.5)), 
              url('https://github.com/ushmaryosep/personal-website-finals-webprog/blob/main/final%20bg.gif?raw=true') no-repeat center center;
  background-size: cover;
  z-index: 70;
}

.content-wrapper {
  width: 100%; max-width: 600px; /* Constrained width to keep it on the left */
  background: rgba(0, 0, 0, 0.7);
  backdrop-filter: blur(8px);
  padding: 30px;
  border-left: 4px solid #f4d03f;
  height: 90vh;
  display: flex;
  flex-direction: column;
}

.messenger-title { font-family: 'Bangers'; color: #f4d03f; font-size: 2rem; margin-bottom: 5px; }
.messenger-subtitle { color: #ccc; font-size: 0.9rem; margin-bottom: 20px; font-family: 'Oswald'; }

.layout-grid {
  display: grid;
  grid-template-columns: 1fr;
  gap: 20px;
  overflow-y: auto;
  padding-right: 10px;
}

h3 { font-family: 'Bangers'; color: #f4d03f; font-size: 1.2rem; margin-bottom: 10px; }

/* Form Styles */
.ledger-form { display: flex; flex-direction: column; gap: 10px; }
.ledger-form input, .ledger-form textarea {
  background: rgba(255,255,255,0.1); border: 1px solid #444; color: white; padding: 10px;
  font-family: 'Oswald'; font-size: 0.9rem; border-radius: 4px;
}
.ledger-form textarea { height: 80px; resize: none; }
.ledger-form button {
  background: #f4d03f; color: black; border: none; padding: 8px;
  font-family: 'Bangers'; font-size: 1.1rem; cursor: pointer;
}

/* Social Buttons */
.social-btns { display: flex; gap: 8px; margin-bottom: 20px; }
.social-link {
  text-decoration: none; color: white; padding: 5px 12px; border: 1px solid #f4d03f;
  font-size: 0.8rem; font-family: 'Oswald'; transition: 0.3s;
}
.social-link:hover { background: #f4d03f; color: black; }

/* Comments Section */
.message-list {
  display: flex; flex-direction: column; gap: 12px;
}
.message-item {
  background: rgba(255,255,255,0.05); padding: 10px; border-radius: 4px; border-left: 2px solid #555;
}
.msg-author { color: #f4d03f; font-weight: bold; font-size: 0.85rem; display: block; margin-bottom: 3px; }
.msg-text { font-size: 0.85rem; color: #ddd; line-height: 1.3; }

.status-text { color: #f4d03f; font-family: 'Bangers'; margin-top: 5px; font-size: 0.9rem; }
.back-to-deck-btn {
  margin-top: auto; background: none; border: 1px solid white; color: white;
  padding: 8px; cursor: pointer; font-family: 'Oswald'; font-size: 0.8rem;
}

/* Scrollbar styling */
.layout-grid::-webkit-scrollbar { width: 4px; }
.layout-grid::-webkit-scrollbar-thumb { background: #f4d03f; }
</style>