<template>
  <div class="soundtrack-screen">
    <div class="soundtrack-container">
      <h1 class="soundtrack-title">🎵 CAPTAIN'S SOUNDTRACK</h1>
      <p class="soundtrack-subtitle">The anthems that fuel the voyage through the Grand Line. <b>Note: This is a Spotify API. Use personal internet connection to access the tracks.</b></p>

      <div v-if="loading" class="spotify-loader">
        <div class="sonar"></div>
        <p>FETCHING LOGS FROM THE DEN DEN MUSHI...</p>
      </div>

      <div v-else class="tracks-list">
        <div v-for="(track, index) in tracks" :key="track.id" class="track-card">
          <span class="track-rank">#{{ index + 1 }}</span>
          <img :src="track.album.images[0].url" class="track-art" />
          <div class="track-info">
            <h3 class="track-name">{{ track.name }}</h3>
            <p class="track-artist">{{ track.artists[0].name }}</p>
          </div>
          <div class="track-player">
            <iframe 
              :src="`https://open.spotify.com/embed/track/${track.id}?utm_source=generator&theme=0`" 
              width="100%" 
              height="80" 
              frameBorder="0" 
              allow="autoplay; clipboard-write; encrypted-media; fullscreen; picture-in-picture" 
              loading="lazy">
            </iframe>
          </div>
        </div>
      </div>

      <button @click="$emit('close')" class="back-to-menu-sound">← BACK TO Captain's Deck</button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      loading: true,
      tracks: [],
      clientId: 'c447c0a3f70444b0bc6ce6a50145b02e',
      clientSecret: '3a13ea955ed84d5a874044653f31fe65',
      myTopTracks: [
        "Bulong December Avenue",
        "Paris in the Rain Lauv",
        "Nothing Bruno Major",
        "I'll Be Edwin McCain",
        "Sparkle RADWIMPS"
      ]
    }
  },
  async mounted() {
    await this.fetchMyTracks();
  },
  methods: {
    async fetchMyTracks() {
      try {
        // 1. Get Access Token from official Spotify Auth
        const authParam = btoa(`${this.clientId}:${this.clientSecret}`);
        const tokenResponse = await fetch('https://accounts.spotify.com/api/token', {
          method: 'POST',
          headers: {
            'Authorization': `Basic ${authParam}`,
            'Content-Type': 'application/x-www-form-urlencoded'
          },
          body: 'grant_type=client_credentials'
        });
        const tokenData = await tokenResponse.json();
        const accessToken = tokenData.access_token;

        // 2. Fetch tracks via official Spotify Search API
        const trackResults = [];
        for (const query of this.myTopTracks) {
          const searchResponse = await fetch(
            `https://api.spotify.com/v1/search?q=${encodeURIComponent(query)}&type=track&limit=1`,
            {
              headers: { 'Authorization': `Bearer ${accessToken}` }
            }
          );
          const data = await searchResponse.json();
          if (data.tracks && data.tracks.items.length > 0) {
            trackResults.push(data.tracks.items[0]);
          }
        }

        this.tracks = trackResults;
        this.loading = false;
      } catch (error) {
        console.error("Spotify voyage failed:", error);
        this.loading = false;
      }
    }
  }
}
</script>

<style scoped>
.soundtrack-screen {
  position: absolute; top: 0; left: 0; width: 100vw; height: 100vh;
  display: flex; justify-content: center; align-items: center; z-index: 60; padding: 40px;
  /* FIXED URL BELOW */
  background: url('https://raw.githubusercontent.com/ushmaryosep/personal-website-finals-webprog/main/assets(gif%2C%20png%2C%20jpg)/green%20bg%20for%20music.gif') no-repeat center center;
  background-size: cover;
}
.soundtrack-container {
  width: 90%; max-width: 850px; height: 85vh; background: rgba(0, 0, 0, 0.85);
  border: 3px solid #1DB954; border-radius: 15px; padding: 40px; 
  display: flex; flex-direction: column; overflow: hidden;
  box-shadow: 0 0 30px rgba(29, 185, 84, 0.3);
}
.soundtrack-title { font-family: 'Bangers'; color: #1DB954; font-size: 3.5rem; text-align: center; margin-bottom: 5px; text-shadow: 3px 3px 0px #000; }
.soundtrack-subtitle { text-align: center; color: #888; margin-bottom: 30px; font-style: italic; }

.tracks-list { flex: 1; overflow-y: auto; display: flex; flex-direction: column; gap: 15px; padding-right: 10px; }
.track-card {
  display: flex; align-items: center; background: rgba(255, 255, 255, 0.05);
  padding: 10px 20px; border-radius: 10px; gap: 20px; transition: 0.3s;
}
.track-card:hover { background: rgba(29, 185, 84, 0.1); transform: scale(1.01); }
.track-rank { font-family: 'Bangers'; font-size: 1.8rem; color: #1DB954; min-width: 40px; }
.track-art { width: 65px; height: 65px; border-radius: 4px; box-shadow: 0 4px 10px rgba(0,0,0,0.5); }
.track-info { flex: 1; min-width: 150px; }
.track-name { font-weight: bold; color: white; font-size: 1.1rem; margin-bottom: 4px; }
.track-artist { color: #aaa; font-size: 0.9rem; }
.track-player { flex: 2; }

.spotify-loader { display: flex; flex-direction: column; align-items: center; justify-content: center; flex: 1; gap: 20px; }
.sonar {
  width: 60px; height: 60px; border: 4px solid #1DB954; border-radius: 50%;
  animation: pulse 1.5s infinite;
}
@keyframes pulse { 0% { transform: scale(0.8); opacity: 1; } 100% { transform: scale(2); opacity: 0; } }

.back-to-menu-sound {
  margin-top: 25px; background: none; border: 2px solid #1DB954; color: #1DB954;
  padding: 12px 35px; font-family: 'Bangers'; font-size: 1.5rem; cursor: pointer; align-self: center;
  transition: 0.3s;
}
.back-to-menu-sound:hover { background: #1DB954; color: black; }
</style>