<template>
  <div id="app" class="grand-line">
    <img 
      src="https://github.com/ushmaryosep/personal-website-finals/blob/main/live%20background.gif?raw=true" 
      class="bg-gif" 
      alt="Grand Line"
    />
    <div class="overlay"></div>

    <div class="stage" :class="{ 'is-shifted': showPoster }">
      
      <section class="screen section-left">
        <div class="content-box">
          <img 
            src="https://raw.githubusercontent.com/ushmaryosep/personal-website-finals/refs/heads/main/hero%20title.png" 
            class="hero-title-img"
            alt="Joshmar Clavero"
          />

          <p class="pirate-description">
            Ahoy, wanderer of the seas! This be the personal stronghold of Joshmar Clavero, 
            where all tales of the captain be gathered—from humble beginnings and 
            Grand Line training, to battle skills, crew pastimes, and glorious achievements.
          </p>

          <button @click="showPoster = true" class="pirate-btn">
            VIEW WANTED POSTER ☠
          </button>
        </div>
      </section>

      <section class="screen section-right">
        <div class="poster-wrap">
          <img 
            src="https://raw.githubusercontent.com/ushmaryosep/personal-website-finals/refs/heads/main/HERO%20CARD.png" 
            class="wanted-card"
            alt="Wanted Poster"
          />
          <button @click="showPoster = false" class="back-btn">
            ← RETURN TO SHIP
          </button>
        </div>
      </section>

    </div>
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      showPoster: false
    }
  }
}
</script>

<style>
/* Reset and Global Styles */
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  background-color: #000;
  overflow: hidden; /* Prevents scrollbars during the slide transition */
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
}

.grand-line {
  position: relative;
  width: 100vw;
  height: 100vh;
}

/* Background Logic */
.bg-gif {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  object-fit: cover;
  z-index: -2;
}

.overlay {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.4); /* Darkens the GIF so text pops */
  z-index: -1;
}

/* Animation Stage Logic */
.stage {
  display: flex;
  width: 200vw; /* Side-by-side sections */
  height: 100vh;
  transition: transform 1.2s cubic-bezier(0.85, 0, 0.15, 1);
}

.is-shifted {
  transform: translateX(-100vw);
}

.screen {
  width: 100vw;
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  padding: 5%;
}

/* --- TITLE & TEXT EFFECTS --- */

.hero-title-img {
  width: 100%;
  max-width: 600px;
  animation: titleZoom 5s ease-in-out infinite;
  filter: drop-shadow(0 0 20px rgba(255, 255, 255, 0.3));
}

@keyframes titleZoom {
  0%, 100% { transform: scale(1); }
  50% { transform: scale(1.08); }
}

.pirate-description {
  color: white;
  font-size: 1.2rem;
  max-width: 600px;
  margin: 30px auto;
  text-align: center;
  text-shadow: 2px 2px 10px rgba(0,0,0,0.9);
  animation: float 4s ease-in-out infinite;
}

@keyframes float {
  0%, 100% { transform: translateY(0); opacity: 0.9; }
  50% { transform: translateY(-10px); opacity: 1; }
}

/* --- PIRATE BUTTON --- */

.pirate-btn {
  background: #f4d03f;
  color: #1a1a1a;
  border: 4px solid #5d4037;
  padding: 15px 40px;
  font-weight: 900;
  font-size: 1.3rem;
  cursor: pointer;
  transition: 0.3s;
  box-shadow: 0 5px 15px rgba(0,0,0,0.5);
}

.pirate-btn:hover {
  background: #fff;
  transform: scale(1.1) rotate(-3deg);
  box-shadow: 0 0 30px rgba(255, 215, 0, 0.6);
}

/* --- WANTED POSTER SECTION --- */

.wanted-card {
  max-height: 80vh;
  max-width: 90%;
  border: 10px solid #2c1a11;
  box-shadow: 0 0 60px rgba(0,0,0,0.9);
}

.back-btn {
  margin-top: 25px;
  background: transparent;
  color: white;
  border: 1px solid white;
  padding: 10px 20px;
  cursor: pointer;
  opacity: 0.7;
  transition: 0.3s;
}

.back-btn:hover { opacity: 1; border-color: #f4d03f; color: #f4d03f; }
</style>