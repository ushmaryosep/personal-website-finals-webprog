<template>
  <div class="resources-screen">
    <div class="resources-scroll">
      <h1 class="resources-title">📜 VOYAGE LOG: RESOURCES</h1>
      <p class="resources-subtitle">The tools and treasures used to build this corner of the Grand Line.</p>

      <div class="resources-grid">
        <div class="res-category">
          <h3>🚀 CORE ENGINE</h3>
          <ul>
            <li><strong>Vue.js 3</strong> - The ship's framework.</li>
            <li><strong>JavaScript (ES6+)</strong> - The logic behind the sails.</li>
            <li><strong>CSS3 & Flexbox/Grid</strong> - Designing the layout of the deck.</li>
          </ul>
        </div>

        <div class="res-category">
          <h3>📡 DEN DEN MUSHI (APIs)</h3>
          <ul>
            <li><strong>Spotify Web API</strong> - Delivering the Captain's anthems.</li>
            <li><strong>OMDB API</strong> - Fetching the legendary movie archives.</li>
            <li><strong>Jikan API</strong> - Scouting the anime seas via MyAnimeList.</li>
            <li><strong>Supabase</strong> - The cloud ledger for the Messenger Deck.</li>
          </ul>
        </div>

        <div class="res-category">
          <h3>🎨 VISUAL TREASURES</h3>
          <ul>
            <li><strong>GitHub Raw</strong> - Hosting the custom GIFs and PNGs.</li>
            <li><strong>Unsplash</strong> - High-quality scenery for the lifestyle deck.</li>
            <li><strong>Flaticon</strong> - Symbols for the social Den Den Mushis.</li>
            <li><strong>Google Fonts</strong> - 'Bangers' and 'Oswald' typography.</li>
          </ul>
        </div>

        <div class="res-category special">
          <h3>🤖 SHIP'S NAVIGATOR</h3>
          <ul>
            <li><strong>Gemini AI</strong> - Technical consulting and code patching.</li>
          </ul>
        </div>
      </div>

      <button @click="$emit('close')" class="back-btn-res">CLOSE LOG</button>
    </div>
  </div>
</template>

<style scoped>
.resources-screen {
  position: absolute; top: 0; left: 0; width: 100vw; height: 100vh;
  background: rgba(0, 0, 0, 0.9);
  display: flex; justify-content: center; align-items: center; z-index: 200;
  padding: 20px;
}
.resources-scroll {
  background: #1a1a1a;
  border: 4px solid #f4d03f;
  border-radius: 15px;
  width: 90%; max-width: 800px;
  max-height: 80vh;
  padding: 40px;
  overflow-y: auto;
  box-shadow: 0 0 50px rgba(244, 208, 63, 0.2);
}
.resources-title { font-family: 'Bangers'; color: #f4d03f; font-size: 3rem; text-align: center; }
.resources-subtitle { text-align: center; color: #888; margin-bottom: 30px; font-style: italic; }

.resources-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 30px;
}
.res-category h3 {
  font-family: 'Bangers';
  color: #f4d03f;
  border-bottom: 1px solid #444;
  padding-bottom: 5px;
  margin-bottom: 15px;
}
.res-category ul { list-style: none; padding: 0; }
.res-category li { color: #ccc; margin-bottom: 10px; font-size: 0.95rem; }
.res-category li strong { color: #fff; }

.special { border: 1px dashed #f4d03f; padding: 15px; border-radius: 8px; background: rgba(244, 208, 63, 0.05); }

.back-btn-res {
  display: block; margin: 30px auto 0;
  background: #f4d03f; color: #000; border: none;
  padding: 10px 30px; font-family: 'Bangers'; font-size: 1.2rem;
  cursor: pointer; transition: 0.3s;
}
.back-btn-res:hover { background: #fff; transform: scale(1.1); }
</style>