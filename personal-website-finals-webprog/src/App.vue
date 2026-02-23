<template>
  <div id="app" class="grand-line">
    <img 
      :src="currentView === 'main' 
        ? 'https://github.com/ushmaryosep/personal-website-finals/blob/main/live%20background.gif?raw=true' 
        : currentView === 'trap' 
        ? 'https://github.com/ushmaryosep/personal-website-finals-webprog/blob/main/bg2.gif?raw=true'
        : 'https://github.com/ushmaryosep/personal-website-finals-webprog/blob/main/main%20menu.gif?raw=true'" 
      class="bg-gif" 
      alt="Grand Line"
    />
    <div class="overlay" :class="{ 'trap-active': currentView === 'trap', 'menu-active': currentView === 'menu' }"></div>

    <transition name="fade">
      <img 
        v-if="showPoster || currentView !== 'main'" 
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
            where all tales of the captain be gathered—from humble beginnings to 
            Grand Line training and glorious achievements.
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
            <button @click="showPoster = false" class="back-btn">← RETURN TO SHIP</button>
            <button @click="triggerTrap" class="marine-btn">REPORT TO MARINES 🏛️</button>
          </div>
        </div>
      </section>
    </div>

    <transition name="zoom-in">
      <div v-if="currentView === 'trap'" class="trap-view">
        <h1 class="trap-title">HA HA! NEVER TRUST A <span class="red">PIRATE!</span></h1>
        
        <div class="fruit-container" @click="currentView = 'menu'">
          <img 
            src="https://github.com/ushmaryosep/personal-website-finals-webprog/blob/main/FRUIT.png?raw=true" 
            class="devil-fruit" 
            alt="Devil Fruit"
          />
          <button class="eat-btn">EAT THIS 🍎</button>
        </div>
      </div>
    </transition>

    <transition name="fade">
      <div v-if="currentView === 'menu'" class="menu-screen-final">
        <div class="stacked-nav">
          <button class="menu-item-stack">🏴‍☠️ Captain’s Deck</button>
          <button class="menu-item-stack">⚓ The Captain’s Tale</button>
          <button class="menu-item-stack">📜 Grand Line Training</button>
          <button class="menu-item-stack">🍖 Crew Pastimes</button>
          <button class="menu-item-stack">🗡️ Battle Abilities</button>
          <button class="menu-item-stack">🏆 Bounties & Glory</button>
          <button class="menu-item-stack">🕊️ Send a Message</button>
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
      currentView: 'main' // main -> trap -> menu
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
/* 1. REFINED FONTS */
@import url('https://fonts.googleapis.com/css2?family=Bangers&family=Oswald:wght@400;700&family=Luckiest+Guy&display=swap');

* { margin: 0; padding: 0; box-sizing: border-box; }
body { background-color: #000; overflow: hidden; font-family: 'Oswald', sans-serif; }

/* LOGO */
.main-logo {
  position: fixed; top: 20px; left: 20px; width: 60px; z-index: 150;
  cursor: pointer; filter: drop-shadow(0 0 10px #f4d03f); transition: 0.3s;
}
.main-logo:hover { transform: scale(1.1) rotate(-5deg); }

.grand-line { position: relative; width: 100vw; height: 100vh; }
.bg-gif { position: absolute; top: 0; left: 0; width: 100%; height: 100%; object-fit: cover; z-index: -2; }

.overlay {
  position: absolute; top: 0; left: 0; width: 100%; height: 100%;
  background: linear-gradient(to right, rgba(0,0,0,0.6) 20%, rgba(0,0,0,0) 100%);
  z-index: -1; transition: 1.5s ease;
}
.overlay.trap-active { background: rgba(0, 0, 0, 0.75); }
.overlay.menu-active { background: rgba(0, 0, 0, 0.2); }

/* SCAM OVERLAY */
.scam-text {
  color: #ff0000; font-family: 'Bangers', cursive; font-size: 5rem;
  margin-bottom: 20px; text-shadow: 0 0 20px black; animation: shake 0.1s infinite;
}

@keyframes shake {
  0% { transform: translate(1px, 1px); }
  50% { transform: translate(-2px, -1px); }
  100% { transform: translate(1px, -2px); }
}

/* STAGE SYSTEM */
.stage { display: flex; width: 200vw; height: 100vh; transition: 1.2s cubic-bezier(0.85, 0, 0.15, 1); }
.is-shifted { transform: translateX(-100vw); }
.screen { width: 100vw; height: 100vh; display: flex; align-items: center; padding-left: 8%; }

.loading-overlay {
  position: fixed; top: 0; left: 0; width: 100vw; height: 100vh;
  background: black; z-index: 200; display: flex; flex-direction: column;
  justify-content: center; align-items: center;
}
.loading-overlay img { width: 100%; height: 70%; object-fit: contain; }

/* TRAP & FRUIT */
.trap-view {
  position: absolute; top: 0; left: 0; width: 100vw; height: 100vh;
  display: flex; flex-direction: column; justify-content: center; align-items: center; z-index: 10;
}
.trap-title {
  font-size: 4rem; color: white; margin-bottom: 40px;
  font-family: 'Luckiest Guy', cursive; text-shadow: 4px 4px 0px #ff0000;
}
.red { color: #ff0000; }

.fruit-container {
  display: flex; flex-direction: column; align-items: center;
  cursor: pointer; transition: 0.3s;
}
.devil-fruit {
  width: 200px; filter: drop-shadow(0 0 15px #a349a4);
  animation: float 3s ease-in-out infinite;
}
.eat-btn {
  margin-top: 20px; background: #f4d03f; border: 4px solid #5d4037;
  font-family: 'Bangers'; font-size: 2rem; padding: 10px 30px; cursor: pointer;
}
.fruit-container:hover { transform: scale(1.1); }

@keyframes float {
  0%, 100% { transform: translateY(0); }
  50% { transform: translateY(-20px); }
}

/* FINAL MENU (FAR RIGHT STACK) */
.menu-screen-final {
  position: absolute; top: 0; right: 0; width: 100vw; height: 100vh;
  display: flex; justify-content: flex-end; align-items: center;
  padding-right: 5%;
}
.stacked-nav {
  display: flex; flex-direction: column; gap: 15px;
}
.menu-item-stack {
  background: rgba(0, 0, 0, 0.7);
  border-left: 5px solid #f4d03f;
  color: white;
  font-family: 'Oswald', sans-serif;
  font-size: 1.1rem;
  font-weight: bold;
  text-transform: uppercase;
  padding: 15px 30px;
  width: 250px;
  text-align: left;
  cursor: pointer;
  transition: all 0.3s ease;
  backdrop-filter: blur(5px);
}
.menu-item-stack:hover {
  background: #f4d03f;
  color: black;
  transform: translateX(-10px);
}

/* MISC UI */
.hero-title-img { width: 100%; max-width: 500px; animation: titleZoom 5s infinite; }
.pirate-description { color: white; margin: 25px 0; max-width: 480px; font-size: 1.2rem; line-height: 1.4; letter-spacing: 0.5px; }
.pirate-btn { background: #f4d03f; padding: 12px 35px; border: 4px solid #5d4037; font-family: 'Bangers'; font-size: 1.5rem; cursor: pointer; }
.wanted-card { max-height: 75vh; border: 8px solid #2c1a11; box-shadow: 0 0 30px rgba(0,0,0,0.8); }
.action-btns { display: flex; gap: 15px; margin-top: 20px; }
.back-btn { background: rgba(0,0,0,0.5); color: white; border: 1px solid white; padding: 10px 20px; cursor: pointer; font-family: 'Oswald'; }
.marine-btn { background: #002d5a; color: white; border: 1px solid white; padding: 10px 20px; cursor: pointer; font-family: 'Oswald'; font-weight: bold; }
.marine-btn:hover { background: #ff0000; }

@keyframes titleZoom { 0%, 100% { transform: scale(1); } 50% { transform: scale(1.03); } }
.fade-leave-active { transition: opacity 0.8s; }
.fade-leave-to { opacity: 0; }
.zoom-in-enter-active { transition: all 0.8s cubic-bezier(0.34, 1.56, 0.64, 1); }
.zoom-in-enter-from { opacity: 0; transform: scale(1.2); }
</style>