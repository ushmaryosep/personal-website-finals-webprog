<template>
  <div class="messenger-screen">
    <div class="messenger-container">
      <h1 class="messenger-title">🕊️ LEAVE A MESSAGE TO CAPTAIN JOSH</h1>
      <p class="messenger-subtitle">Send a carrier pigeon or log your entry in the Captain's Ledger.</p>

      <div class="messenger-grid">
        <div class="social-links-card">
          <h3>CONNECT VIA DEN DEN MUSHI</h3>
          <div class="social-btns">
            <a href="https://www.facebook.com/joshmar.clavero" target="_blank" class="social-link fb">FACEBOOK</a>
            <a href="https://www.instagram.com/ushmaryosep/" target="_blank" class="social-link ig">INSTAGRAM</a>
            <a href="https://www.linkedin.com/in/joshmar-clavero-8b1912322/" target="_blank" class="social-link li">LINKEDIN</a>
            <a href="https://github.com/ushmaryosep" target="_blank" class="social-link gh">GITHUB</a>
            <a href="mailto:jmclavero25@gmail.com" class="social-link mail">PERSONAL EMAIL</a>
            <a href="mailto:jlclavero@student.apc.edu.ph" class="social-link school">SCHOOL EMAIL</a>
          </div>
        </div>

        <div class="ledger-card">
          <h3>SHIP'S LEDGER</h3>
          <form @submit.prevent="sendMessage" class="ledger-form">
            <input 
              v-model="messengerName" 
              type="text" 
              placeholder="Your Name / Crew Name" 
              required 
            />
            <textarea 
              v-model="messageContent" 
              placeholder="Leave your message for the Captain..." 
              required
            ></textarea>
            <button type="submit" :disabled="isSending">
              {{ isSending ? 'SENDING...' : 'LOG MESSAGE ⚓' }}
            </button>
          </form>
          <p v-if="statusMsg" class="status-text">{{ statusMsg }}</p>
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
      statusMsg: '',
      // Your integrated Supabase credentials
      supabaseUrl: 'https://obexkjwpjkqqiozdaezv.supabase.co', 
      supabaseAnonKey: 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6Im9iZXhrandwamtxcWlvemRhZXp2Iiwicm9sZSI6ImFub24iLCJpYXQiOjE3NzE4NjYwMjgsImV4cCI6MjA4NzQ0MjAyOH0.daEcBIw4qHEQXTMA7yU0JMS2g5kjLEceEpiiYutZdRk'
    }
  },
  methods: {
    async sendMessage() {
      this.isSending = true;
      this.statusMsg = "";
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
          this.statusMsg = "MESSAGE LOGGED IN THE LEDGER!";
          this.messengerName = '';
          this.messageContent = '';
        } else {
          throw new Error("Failed to send");
        }
      } catch (error) {
        this.statusMsg = "THE CARRIER PIGEON GOT LOST. TRY AGAIN!";
        console.error("Supabase Error:", error);
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
  display: flex; justify-content: center; align-items: center; z-index: 70; padding: 20px;
  background: url('https://github.com/ushmaryosep/personal-website-finals-webprog/blob/main/final%20bg.gif?raw=true') no-repeat center center;
  background-size: cover;
}
.messenger-container {
  width: 95%; max-width: 900px; background: rgba(20, 20, 20, 0.9); backdrop-filter: blur(10px);
  border: 3px solid #f4d03f; border-radius: 15px; padding: 40px; color: white;
  box-shadow: 0 0 30px rgba(244, 208, 63, 0.4);
}
.messenger-title { font-family: 'Bangers'; color: #f4d03f; font-size: 2.8rem; text-align: center; text-shadow: 2px 2px 0 #000; }
.messenger-subtitle { text-align: center; color: #ccc; margin-bottom: 30px; font-family: 'Oswald'; }
.messenger-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 40px; }

.social-links-card h3, .ledger-card h3 { font-family: 'Bangers'; margin-bottom: 20px; color: #f4d03f; letter-spacing: 1px; }
.social-btns { display: grid; grid-template-columns: 1fr 1fr; gap: 10px; }
.social-link {
  text-decoration: none; color: white; padding: 10px; border: 1px solid #444;
  text-align: center; font-family: 'Oswald'; font-size: 0.9rem; transition: 0.3s; background: rgba(0,0,0,0.6);
}
.social-link:hover { background: #f4d03f; color: black; border-color: #f4d03f; transform: translateY(-3px); }

.ledger-form { display: flex; flex-direction: column; gap: 15px; }
.ledger-form input, .ledger-form textarea {
  background: rgba(255,255,255,0.1); border: 1px solid #444; color: white; padding: 12px;
  font-family: 'Oswald'; border-radius: 5px; outline: none;
}
.ledger-form input:focus, .ledger-form textarea:focus { border-color: #f4d03f; }
.ledger-form textarea { height: 120px; resize: none; }
.ledger-form button {
  background: #f4d03f; color: black; border: none; padding: 12px;
  font-family: 'Bangers'; font-size: 1.4rem; cursor: pointer; transition: 0.3s;
}
.ledger-form button:hover:not(:disabled) { background: white; transform: scale(1.02); }

.status-text { margin-top: 15px; color: #f4d03f; text-align: center; font-family: 'Bangers'; letter-spacing: 1px; }
.back-to-deck-btn {
  margin-top: 30px; background: none; border: 2px solid #f4d03f; color: #f4d03f;
  padding: 10px 30px; align-self: center; cursor: pointer; font-family: 'Bangers'; font-size: 1.2rem;
}
.back-to-deck-btn:hover { background: #f4d03f; color: black; }

@media (max-width: 768px) {
  .messenger-grid { grid-template-columns: 1fr; }
  .messenger-container { height: 90vh; overflow-y: auto; }
}
</style>