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
        <div class="content-box left-aligned">
          <img 
            src="https://raw.githubusercontent.com/ushmaryosep/personal-website-finals/refs/heads/main/hero%20title.png" 
            class="hero-title-img"
            alt="Joshmar Clavero"
          />

          <p class="pirate-description text-left">
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
        <div class="poster-wrap left-aligned-poster">
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
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  background-color: #000;
  overflow: hidden;
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
}

.grand-line {
  position: relative;
  width: 100vw;
  height: 100vh;
}

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
  background: linear-gradient(to right, rgba(0,0,0,0.7) 30%, rgba(0,0,0,0.2) 100%);
  z-index: -1;
}

.stage {
  display: flex;
  width: 200vw;
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
  align-items: center; /* Vertical center */
  justify-content: flex-start; /* Push to left */
  padding-left: 8%; /* Adjust this to move further left/right */
}

/* --- NEW POSITIONING CLASSES --- */

.left-aligned {
  text-align: left;
  max-width: 550px;
}

.left-aligned-poster {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
}

/* --- TITLE & TEXT --- */

.hero-title-img {
  width: 100%;
  max-width: 500px;
  animation: titleZoom 5s ease-in-out infinite;
  filter: drop-shadow(0 0 20px rgba(255, 255, 255, 0.3));
}

@keyframes titleZoom {
  0%, 100% { transform: scale(1); }
  50% { transform: scale(1.05); }
}

.pirate-description {
  color: white;
  font-size: 1.1rem;
  margin: 25px 0;
  text-shadow: 2px 2px 8px rgba(0,0,0,1);
  line-height: 1.6;
}

/* --- BUTTONS --- */

.pirate-btn {
  background: #f4d03f;
  color: #1a1a1a;
  border: 4px solid #5d4037;
  padding: 12px 35px;
  font-weight: 900;
  font-size: 1.1rem;
  cursor: pointer;
  transition: 0.3s;
}

.pirate-btn:hover {
  background: #fff;
  transform: translateY(-3px);
}

/* --- POSTER --- */

.wanted-card {
  max-height: 75vh;
  width: auto;
  border: 8px solid #2c1a11;
  box-shadow: 0 0 40px rgba(0,0,0,0.8);
}

.back-btn {
  margin-top: 20px;
  background: rgba(0,0,0,0.5);
  color: white;
  border: 1px solid white;
  padding: 8px 15px;
  cursor: pointer;
  transition: 0.3s;
}

.back-btn:hover { color: #f4d03f; border-color: #f4d03f; }

/* Responsive: Center things on mobile */
@media (max-width: 900px) {
  .screen {
    justify-content: center;
    padding-left: 5%;
    padding-right: 5%;
  }
  .left-aligned, .left-aligned-poster {
    align-items: center;
    text-align: center;
  }
}
</style>