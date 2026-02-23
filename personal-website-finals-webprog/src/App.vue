<template>
  <div id="app" class="grand-line">
    <img src="https://github.com/ushmaryosep/personal-website-finals/blob/main/live%20background.gif?raw=true" class="bg-gif" />
    <div class="overlay"></div>

    <div class="stage" :class="{ 'is-shifted': showPoster }">
      
      <section class="screen section-left">
        <div class="content-container">
          <img src="https://raw.githubusercontent.com/ushmaryosep/personal-website-finals/refs/heads/main/hero%20title.png" class="hero-title" />
          <p class="description">
            Ahoy! This be the personal stronghold of Joshmar Clavero. Explore the captain's log, 
            skills, and achievements. Join the crew by leaving a mark in the guestbook below!
          </p>
          <div class="btn-group">
            <button @click="showPoster = true" class="pirate-btn">VIEW WANTED POSTER ☠</button>
            <button @click="scrollToGuestbook" class="pirate-btn secondary">JOIN THE CREW</button>
          </div>
        </div>

        <div id="guestbook" class="guestbook-container">
          <h2 class="pirate-font">THE CAPTAIN'S LOG</h2>
          <form @submit.prevent="addEntry" class="guest-form">
            <input v-model="newName" placeholder="Pirate Name..." required />
            <textarea v-model="newMessage" placeholder="Leave a message..." required></textarea>
            <button type="submit" :disabled="loading" class="submit-btn">POST BOUNTY</button>
          </form>

          <div class="messages-list">
            <div v-for="entry in entries" :key="entry.id" class="message-card">
              <span class="entry-name">{{ entry.name }}:</span>
              <p class="entry-text">{{ entry.message }}</p>
            </div>
          </div>
        </div>
      </section>

      <section class="screen section-right">
        <div class="poster-wrap">
          <img src="https://raw.githubusercontent.com/ushmaryosep/personal-website-finals/refs/heads/main/HERO%20CARD.png" class="wanted-card" />
          <button @click="showPoster = false" class="back-btn">← RETURN TO SHIP</button>
        </div>
      </section>
    </div>
  </div>
</template>

<script>
import { createClient } from '@supabase/supabase-js'

const supabase = createClient('YOUR_SUPABASE_URL', 'YOUR_SUPABASE_KEY')

export default {
  data() {
    return {
      showPoster: false,
      loading: false,
      entries: [],
      newName: '',
      newMessage: ''
    }
  },
  methods: {
    async fetchEntries() {
      const { data } = await supabase.from('guestbook').select('*').order('created_at', { ascending: false })
      this.entries = data || []
    },
    async addEntry() {
      this.loading = true
      const { error } = await supabase.from('guestbook').insert([{ name: this.newName, message: this.newMessage }])
      if (!error) {
        this.newName = ''
        this.newMessage = ''
        await this.fetchEntries()
      }
      this.loading = false
    },
    scrollToGuestbook() {
      document.getElementById('guestbook').scrollIntoView({ behavior: 'smooth' });
    }
  },
  mounted() {
    this.fetchEntries()
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Bangers&display=swap');

* { margin: 0; padding: 0; box-sizing: border-box; }
body { overflow-x: hidden; background: #000; font-family: sans-serif; }

.grand-line { position: relative; width: 100vw; height: 100vh; overflow: hidden; }
.bg-gif { position: absolute; width: 100%; height: 100%; object-fit: cover; z-index: -2; }
.overlay { position: absolute; width: 100%; height: 100%; background: rgba(0,0,0,0.5); z-index: -1; }

.stage { display: flex; width: 200vw; height: 100vh; transition: transform 1s cubic-bezier(0.85, 0, 0.15, 1); }
.is-shifted { transform: translateX(-100vw); }

.screen { width: 100vw; height: 100vh; overflow-y: auto; display: flex; flex-direction: column; align-items: center; padding: 40px 20px; color: white; }
.hero-title { width: 100%; max-width: 500px; animation: zoom 4s infinite ease-in-out; margin-bottom: 20px; }

@keyframes zoom { 0%, 100% { transform: scale(1); } 50% { transform: scale(1.05); } }

.description { max-width: 600px; margin-bottom: 30px; text-align: center; line-height: 1.6; text-shadow: 2px 2px 4px #000; }

.pirate-btn { padding: 12px 25px; background: #ffcc00; border: 3px solid #5d4037; font-family: 'Bangers', cursive; font-size: 1.2rem; cursor: pointer; color: black; transition: 0.3s; margin: 10px; }
.pirate-btn:hover { background: white; transform: rotate(-2deg) scale(1.1); }

.guestbook-container { margin-top: 50px; width: 100%; max-width: 500px; background: rgba(0,0,0,0.8); padding: 20px; border: 2px solid #ffcc00; }
.pirate-font { font-family: 'Bangers', cursive; color: #ffcc00; margin-bottom: 15px; }
.guest-form input, .guest-form textarea { width: 100%; padding: 10px; margin: 10px 0; background: #eee; border: none; }
.submit-btn { width: 100%; padding: 10px; background: #d32f2f; color: white; border: none; font-weight: bold; cursor: pointer; }

.wanted-card { max-height: 75vh; border: 8px solid #333; }
.back-btn { margin-top: 20px; color: white; background: none; border: 1px solid white; padding: 10px; cursor: pointer; }
</style>