<template>
  <div id="app" class="grand-line">
    <img 
      :src="currentView === 'main' 
        ? 'https://github.com/ushmaryosep/personal-website-finals/blob/main/live%20background.gif?raw=true' 
        : 'https://github.com/ushmaryosep/personal-website-finals-webprog/blob/main/bg2.gif?raw=true'" 
      class="bg-gif" 
      alt="Grand Line"
    />
    <div class="overlay" :class="{ 'trap-active': currentView === 'trap' }"></div>

    <transition name="fade">
      <img 
        v-if="showPoster || currentView === 'trap'" 
        src="https://github.com/ushmaryosep/personal-website-finals-webprog/blob/main/mylogo.png?raw=true" 
        class="main-logo"
        @click="resetToHome"
        alt="Logo"
      />
    </transition>

    <transition name="fade">
      <div v-if="isLoading" class="loading-overlay">
        <h1 class="scam-text">YOU'VE BEEN SCAMMED!</h1>
        <img src="https://github.com/ushmaryosep/personal-website-finals-webprog/blob/main/loading%20screen.gif?raw=true" alt="Loading..." />
      </div>
    </transition>

    <div v-if="currentView === 'main'" class="stage" :class="{ 'is-shifted': showPoster }">
      
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
          <div class="action-btns">
            <button @click="showPoster = false" class="back-btn">
              ← RETURN TO SHIP
            </button>
            <button @click="triggerTrap" class="marine-btn">
              REPORT TO MARINES 🏛️
            </button>
          </div>
        </div>
      </section>
    </div>

    <transition name="zoom-in">
      <div v-if="currentView === 'trap'" class="trap-view">
        <h1 class="trap-title">HA HA! NEVER TRUST A <span class="red">PIRATE!</span></h1>
        
        <div class="nav-grid">
          <button class="menu-item pirate-font">🏴‍☠️ Captain’s Deck</button>
          <button class="menu-item pirate-font">⚓ The Captain’s Tale</button>
          <button class="menu-item pirate-font">📜 Grand Line Training</button>
          <button class="menu-item pirate-font">🍖 Crew Pastimes</button>
          <button class="menu-item pirate-font">🗡️ Battle Abilities</button>
          <button class="menu-item pirate-font">🏆 Bounties & Glory</button>
          <button class="menu-item pirate-font">🕊️ Send a Den Den Message</button>
        </div>
      </div>
    </transition>

  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      showPoster: false,
      isLoading: false,
      currentView: 'main' 
    }
  },
  methods: {
    triggerTrap() {
      this.isLoading = true;
      setTimeout(() => {
        this.isLoading = false;
        this.currentView = 'trap';
      }, 2200);
    },
    resetToHome() {
      this.currentView = 'main';
      this.showPoster = false;
    }
  }
}
</script>

<style>
/* 1. IMPORT GOOGLE FONTS */
@import url('https://fonts.googleapis.com/css2?family=Bangers&family=Luckiest+Guy&display=swap');

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

/* 2. LOGO STYLING */
.main-logo {
  position: fixed;
  top: 20px;
  left: 20px;
  width: 60px;
  z-index: 150;
  cursor: pointer;
  filter: drop-shadow(0 0 10px #f4d03f);
  transition: 0.3s;
}
.main-logo:hover { transform: scale(1.1) rotate(-5deg); }

.grand-line {
  position: relative;
  width: 100vw;
  height: 100vh;
}

.bg-gif {
  position: absolute;
  top: 0; left: 0;
  width: 100%; height: 100%;
  object-fit: cover;
  z-index: -2;
}

.overlay {
  position: absolute;
  top: 0; left: 0;
  width: 100%; height: 100%;
  background: linear-gradient(to right, rgba(0,0,0,0.7) 30%, rgba(0,0,0,0.2) 100%);
  z-index: -1;
  transition: background 1.5s ease;
}

.overlay.trap-active {
  background: rgba(0, 0, 0, 0.7);
}

/* 3. SCAMMED TEXT ANIMATION */
.scam-text {
  color: #ff0000;
  font-family: 'Bangers', cursive;
  font-size: 5rem;
  margin-bottom: 20px;
  text-shadow: 0 0 20px black;
  animation: shake 0.1s infinite;
}

@keyframes shake {
  0% { transform: translate(1px, 1px); }
  50% { transform: translate(-2px, -1px); }
  100% { transform: translate(1px, -2px); }
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
  align-items: center;
  justify-content: flex-start;
  padding-left: 8%;
}

.loading-overlay {
  position: fixed;
  top: 0; left: 0;
  width: 100vw; height: 100vh;
  background: black;
  z-index: 200;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.loading-overlay img {
  width: 100%;
  height: 70%;
  object-fit: contain;
}

.trap-view {
  position: absolute;
  top: 0; left: 0;
  width: 100vw; height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  z-index: 10;
  text-align: center;
}

.trap-title {
  font-size: 4rem;
  color: white;
  margin-bottom: 40px;
  font-family: 'Luckiest Guy', cursive;
  text-shadow: 4px 4px 0px #ff0000;
}

.red { color: #ff0000; }

.nav-grid {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 15px;
  width: 90%;
  max-width: 800px;
}

/* 4. IMPROVED PIRATE BUTTONS */
.menu-item.pirate-font {
  font-family: 'Bangers', cursive;
  padding: 15px;
  background: rgba(0, 0, 0, 0.8);
  border: 2px solid #f4d03f;
  color: #f4d03f;
  font-size: 1.5rem;
  letter-spacing: 2px;
  cursor: pointer;
  transition: 0.3s;
}

.menu-item:hover {
  background: #f4d03f;
  color: #000;
  transform: translateY(-5px);
  box-shadow: 0 10px 20px rgba(244, 208, 63, 0.4);
}

.action-btns {
  display: flex;
  gap: 15px;
  margin-top: 20px;
}

.marine-btn {
  background: #002d5a;
  color: white;
  border: 1px solid white;
  padding: 8px 15px;
  cursor: pointer;
  font-weight: bold;
  transition: 0.3s;
}

.marine-btn:hover {
  background: #ff0000;
  border-color: #ff0000;
}

.fade-leave-active { transition: opacity 0.8s; }
.fade-leave-to { opacity: 0; }

.zoom-in-enter-active { transition: all 0.8s cubic-bezier(0.34, 1.56, 0.64, 1); }
.zoom-in-enter-from { opacity: 0; transform: scale(1.2); }

.left-aligned { text-align: left; max-width: 550px; }
.left-aligned-poster { display: flex; flex-direction: column; align-items: flex-start; }
.hero-title-img { width: 100%; max-width: 500px; animation: titleZoom 5s infinite; }
.pirate-description { color: white; margin: 25px 0; }
.pirate-btn { background: #f4d03f; padding: 12px 35px; border: 4px solid #5d4037; font-weight: 900; cursor: pointer; }
.wanted-card { max-height: 75vh; border: 8px solid #2c1a11; }
.back-btn { background: rgba(0,0,0,0.5); color: white; border: 1px solid white; padding: 8px 15px; cursor: pointer; }

@keyframes titleZoom { 0%, 100% { transform: scale(1); } 50% { transform: scale(1.05); } }
</style>