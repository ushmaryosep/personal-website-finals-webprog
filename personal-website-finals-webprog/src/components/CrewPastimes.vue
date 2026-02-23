<template>
  <div class="pastimes-screen">
    <div class="pastimes-container">
      <div class="header-area">
        <button @click="$emit('close')" class="back-to-deck">← RETURN TO SHIP</button>
        <h1 class="pastimes-title">🍖 CREW PASTIMES</h1>
        <p class="subtitle">Even the fiercest captains need time off the battlefield.</p>
      </div>

      <div class="lifestyle-grid">
        <div class="hobby-card gym">
          <div class="hobby-overlay">
            <span class="icon">🏋️</span>
            <h3>Gym Training</h3>
            <p>Sharpening strength and discipline. Every rep builds not just muscle — but mindset.</p>
          </div>
        </div>

        <div class="hobby-card moto">
          <div class="hobby-overlay">
            <span class="icon">🏍️</span>
            <h3>Motorcycles</h3>
            <p>Speed. Freedom. The feeling of owning the road like a true pirate of the highways.</p>
          </div>
        </div>

        <div class="hobby-card food">
          <div class="hobby-overlay">
            <span class="icon">🍗</span>
            <h3>Food Adventures</h3>
            <p>From local street feasts to legendary meals — fueling the captain properly is serious business.</p>
          </div>
        </div>

        <div class="hobby-card cars">
          <div class="hobby-overlay">
            <span class="icon">🚗</span>
            <h3>Cars</h3>
            <p>Power, engineering, design — machines that roar like sea beasts.</p>
          </div>
        </div>
      </div>

      <div class="media-header">
        <h2 class="section-label">🎬 STRATEGY & IMAGINATION (MOVIES + ANIME)</h2>
      </div>

      <div v-if="loading" class="loading-state">
        <div class="spinner"></div>
        <p>SCOUTING THE GRAND LINE FOR MEDIA...</p>
      </div>

      <div v-else class="media-grid">
        <div class="media-row">
          <h3 class="row-title">MASTERPIECES (Movies)</h3>
          <div class="scroll-box">
            <div v-for="movie in movies" :key="movie.imdbID" class="api-card">
              <img :src="movie.Poster" :alt="movie.Title" />
              <div class="api-card-content">
                <h4>{{ movie.Title }}</h4>
                <p>Year: {{ movie.Year }} • ⭐ {{ movie.imdbRating }}</p>
              </div>
            </div>
          </div>
        </div>

        <div class="media-row">
          <h3 class="row-title">ANIME LOGS</h3>
          <div class="scroll-box">
            <div v-for="item in anime" :key="item.mal_id" class="api-card">
              <img :src="item.images.jpg.large_image_url" :alt="item.title" />
              <div class="api-card-content">
                <h4>{{ item.title }}</h4>
                <p>Score: {{ item.score }} / 10</p>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      movies: [],
      anime: [],
      loading: true,
      OMDB_KEY: '58d83f96'
    }
  },
  async mounted() {
    await this.fetchMedia();
  },
  methods: {
    async fetchMedia() {
      try {
        const movieTitles = [
          { t: "The Count of Monte Cristo", y: "2002" },
          { t: "The Notebook", y: "2004" },
          { t: "Amadeus", y: "1984" }
        ];
        const moviePromises = movieTitles.map(m => 
          fetch(`https://www.omdbapi.com/?apikey=${this.OMDB_KEY}&t=${encodeURIComponent(m.t)}&y=${m.y}`).then(res => res.json())
        );
        this.movies = await Promise.all(moviePromises);

        const animeTitles = ["Baccano!", "Capeta", "Steins;Gate"];
        for (const title of animeTitles) {
          const res = await fetch(`https://api.jikan.moe/v4/anime?q=${encodeURIComponent(title)}&limit=1`);
          const json = await res.json();
          if (json.data && json.data.length > 0) this.anime.push(json.data[0]);
          await new Promise(r => setTimeout(r, 600)); 
        }
      } catch (err) {
        console.error("API Error:", err);
      } finally {
        this.loading = false;
      }
    }
  }
}
</script>

<style scoped>
.pastimes-screen {
  position: fixed; top: 0; left: 0; width: 100vw; height: 100vh;
  background: linear-gradient(rgba(0,0,0,0.8), rgba(0,0,0,0.9)), 
              url('https://github.com/ushmaryosep/personal-website-finals-webprog/blob/main/BG%203.gif?raw=true');
  background-size: cover; z-index: 100; overflow-y: auto; color: white;
}

.pastimes-container { max-width: 1200px; margin: 0 auto; padding: 60px 20px; }

.header-area { text-align: center; margin-bottom: 50px; }
.back-to-deck { background: none; border: 1px solid #f4d03f; color: #f4d03f; padding: 8px 20px; cursor: pointer; margin-bottom: 20px; }
.pastimes-title { font-family: 'Bangers'; font-size: 4.5rem; color: #f4d03f; text-shadow: 4px 4px 0px #000; }
.subtitle { font-size: 1.2rem; color: #ccc; font-style: italic; }

/* Lifestyle Cards */
.lifestyle-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(250px, 1fr)); gap: 20px; margin-bottom: 60px; }
.hobby-card { 
  height: 300px; border: 2px solid #333; position: relative; overflow: hidden;
  background-size: cover; background-position: center; border-radius: 8px;
}
.gym { background-image: url('https://images.unsplash.com/photo-1534438327276-14e5300c3a48?q=80&w=500'); }
.moto { background-image: url('https://images.unsplash.com/photo-1558981806-ec527fa84c39?q=80&w=500'); }
.food { background-image: url('https://images.unsplash.com/photo-1504674900247-0877df9cc836?q=80&w=500'); }
.cars { background-image: url('https://images.unsplash.com/photo-1503376780353-7e6692767b70?q=80&w=500'); }

.hobby-overlay {
  position: absolute; bottom: 0; width: 100%; padding: 20px;
  background: linear-gradient(transparent, rgba(0,0,0,0.9));
}
.icon { font-size: 2rem; }
.hobby-card h3 { font-family: 'Bangers'; color: #f4d03f; margin: 10px 0; }
.hobby-card p { font-size: 0.9rem; color: #ddd; line-height: 1.4; }

/* Media Section */
.section-label { font-family: 'Bangers'; font-size: 2rem; color: #f4d03f; border-bottom: 2px solid #f4d03f; display: inline-block; margin-bottom: 30px; }
.media-row { margin-bottom: 40px; }
.row-title { font-size: 1.5rem; margin-bottom: 15px; color: #fff; }
.scroll-box { display: flex; gap: 20px; overflow-x: auto; padding-bottom: 15px; }

.api-card { flex: 0 0 220px; background: #111; border-radius: 5px; border: 2px solid #222; transition: 0.3s; }
.api-card:hover { border-color: #f4d03f; transform: scale(1.05); }
.api-card img { width: 100%; height: 300px; object-fit: cover; border-bottom: 2px solid #222; }
.api-card-content { padding: 12px; }
.api-card-content h4 { font-size: 1rem; color: #f4d03f; margin-bottom: 5px; white-space: nowrap; overflow: hidden; text-overflow: ellipsis; }
.api-card-content p { font-size: 0.8rem; color: #888; }

.loading-state { text-align: center; padding: 50px; color: #f4d03f; font-family: 'Bangers'; font-size: 1.5rem; }
</style>