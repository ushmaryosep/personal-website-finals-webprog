<template>
  <div id="app" class="grand-line">
    
    <div class="bg-container">
      <img src="https://github.com/ushmaryosep/personal-website-finals/blob/main/live%20background.gif?raw=true" 
        class="bg-layer" :class="{ 'visible': currentView === 'main' }"/>
      <img src="https://github.com/ushmaryosep/personal-website-finals-webprog/blob/main/bg2.gif?raw=true" 
        class="bg-layer" :class="{ 'visible': currentView === 'trap' }"/>
      <img src="https://github.com/ushmaryosep/personal-website-finals-webprog/blob/main/main%20menu.gif?raw=true" 
        class="bg-layer" :class="{ 'visible': currentView === 'menu' }"/>
      <img src="https://github.com/ushmaryosep/personal-website-finals-webprog/blob/main/BG%203.gif?raw=true" 
        class="bg-layer" :class="{ 'visible': currentView === 'tale' }"/>
    </div>

    <div class="overlay" :class="{ 
      'trap-active': currentView === 'trap', 
      'menu-active': currentView === 'menu' || currentView === 'tale' 
    }"></div>

    <transition name="fade">
      <div v-if="isLoading" class="loading-overlay" :style="loadingType === 'nullify' ? 'background: black;' : ''">
        <template v-if="loadingType === 'scam'">
          <h1 class="scam-text">YOU'VE BEEN SCAMMED!</h1>
          <img src="https://github.com/ushmaryosep/personal-website-finals-webprog/blob/main/loading%20screen.gif?raw=true" alt="Loading..." />
        </template>
        <template v-else>
          <h1 class="nullify-text">EFFECTS NOW NULLIFYING...</h1>
          <img src="https://github.com/ushmaryosep/personal-website-finals-webprog/blob/main/nullifying%20effects.gif?raw=true" class="nullify-gif" />
        </template>
      </div>
    </transition>

    <transition name="fade">
      <img v-if="showPoster || currentView !== 'main'" 
        src="https://github.com/ushmaryosep/personal-website-finals-webprog/blob/main/mylogo.png?raw=true" 
        class="main-logo" @click="resetToHome" />
    </transition>

    <div v-if="currentView === 'main'" class="stage" :class="{ 'is-shifted': showPoster }">
      <section class="screen section-left">
        <div class="content-box left-aligned">
          <img src="https://raw.githubusercontent.com/ushmaryosep/personal-website-finals/refs/heads/main/hero%20title.png" class="hero-title-img" />
          <p class="pirate-description">Ahoy, wanderer of the seas! This be the personal stronghold of Joshmar Clavero, where all tales of the captain be gathered.</p>
          <button @click="showPoster = true" class="pirate-btn">VIEW WANTED POSTER ☠</button>
        </div>
      </section>
      <section class="screen section-right">
        <div class="poster-wrap left-aligned-poster">
          <img src="https://raw.githubusercontent.com/ushmaryosep/personal-website-finals/refs/heads/main/HERO%20CARD.png" class="wanted-card" />
          <div class="action-btns">
            <button @click="showPoster = false" class="back-btn">← RETURN TO SHIP</button>
            <button @click="triggerScam" class="marine-btn">REPORT TO MARINES 🏛️</button>
          </div>
        </div>
      </section>
    </div>

    <transition name="zoom-in">
      <div v-if="currentView === 'trap'" class="trap-view">
        <h1 class="trap-title">HA HA! NEVER TRUST A <span class="red">PIRATE!</span></h1>
        <div class="fruit-container" @click="triggerNullify">
          <img src="https://github.com/ushmaryosep/personal-website-finals-webprog/blob/main/FRUIT.png?raw=true" class="devil-fruit" />
          <button class="eat-btn">EAT THIS 🍎</button>
        </div>
      </div>
    </transition>

    <transition name="fade">
      <div v-if="currentView === 'tale'" class="tale-screen">
        <div class="tale-container">
          <div class="tale-content">
            <img src="https://github.com/ushmaryosep/personal-website-finals-webprog/blob/main/captain's%20tale.png?raw=true" class="tale-title-img-large anim-float" />
            <div class="tale-scroll">
              <p>Ahoy. I be <strong>Joshmar Clavero</strong>, a second-year Information Technology cadet sailing under the banner of Asia Pacific College...</p>
              <p>My passion lies in all things computers — from coding and system building to understanding how technology shapes modern society...</p>
              <p class="mission-text">Beyond ambition, I carry a deeper mission: To rise, to build wealth, and to become a billionaire — not for glory alone, but to secure the future of my parents and siblings.</p>
              <p>I believe technology is power — and power, when guided by purpose, can change lives.</p>
            </div>
            <button @click="currentView = 'menu'" class="back-to-menu">← BACK TO NAV NAVI</button>
          </div>

          <div class="carousel-section">
            <div class="carousel-frame">
              <transition name="fade" mode="out-in">
                <img :src="carouselImages[currentImgIndex]" :key="currentImgIndex" class="carousel-img" @click="isLightboxOpen = true" />
              </transition>
              <div class="carousel-controls">
                <button @click="prevImg">◀</button>
                <span>{{ currentImgIndex + 1 }} / {{ carouselImages.length }}</span>
                <button @click="nextImg">▶</button>
              </div>
            </div>
          </div>
        </div>
      </div>
    </transition>

    <transition name="fade">
      <div v-if="currentView === 'menu'" class="menu-screen-final">
        <div class="menu-wrapper">
          <h2 class="menu-main-title">WELCOME TO THE CAPTAIN'S DECK</h2>
          <div class="stacked-nav">
            <button class="menu-item-stack" @click="currentView = 'tale'">⚓ The Captain’s Tale</button>
            <button class="menu-item-stack">📜 Grand Line Training</button>
            <button class="menu-item-stack">🍖 Crew Pastimes</button>
            <button class="menu-item-stack">🗡️ Battle Abilities</button>
            <button class="menu-item-stack">🏆 Bounties & Glory</button>
            <button class="menu-item-stack">🕊️ Send a Message</button>
          </div>
        </div>
      </div>
    </transition>

    <div v-if="isLightboxOpen" class="lightbox" @click="isLightboxOpen = false">
      <img :src="carouselImages[currentImgIndex]" class="lightbox-content" />
    </div>

  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      showPoster: false,
      isLoading: false,
      loadingType: 'scam', // 'scam' or 'nullify'
      currentView: 'main',
      currentImgIndex: 0,
      isLightboxOpen: false,
      autoScrollTimer: null, // ADDED FOR AUTO-SCROLL
      carouselImages: [
        'https://github.com/ushmaryosep/personal-website-finals-webprog/blob/main/mypic1.png?raw=true',
        'https://github.com/ushmaryosep/personal-website-finals-webprog/blob/main/mypic2.png?raw=true',
        'https://github.com/ushmaryosep/personal-website-finals-webprog/blob/main/mypic3.png?raw=true',
        'https://github.com/ushmaryosep/personal-website-finals-webprog/blob/main/mypic4.png?raw=true',
        'https://github.com/ushmaryosep/personal-website-finals-webprog/blob/main/mypic5.png?raw=true',
        'https://github.com/ushmaryosep/personal-website-finals-webprog/blob/main/mypic6.png?raw=true'
      ]
    }
  },
  methods: {
    triggerScam() {
      this.loadingType = 'scam';
      this.isLoading = true;
      setTimeout(() => { this.isLoading = false; this.currentView = 'trap'; }, 2200);
    },
    // ADDED TRIGGER NULLIFY METHOD
    triggerNullify() {
      this.loadingType = 'nullify';
      this.isLoading = true;
      setTimeout(() => { this.isLoading = false; this.currentView = 'menu'; }, 3000);
    },
    resetToHome() { this.currentView = 'main'; this.showPoster = false; },
    nextImg() { this.currentImgIndex = (this.currentImgIndex + 1) % this.carouselImages.length; },
    prevImg() { this.currentImgIndex = (this.currentImgIndex - 1 + this.carouselImages.length) % this.carouselImages.length; },
    // ADDED START/STOP AUTO SCROLL
    startAutoScroll() {
      this.autoScrollTimer = setInterval(this.nextImg, 3000);
    },
    stopAutoScroll() {
      clearInterval(this.autoScrollTimer);
    }
  },
  // ADDED WATCHER FOR AUTO-SCROLL
  watch: {
    currentView(newVal) {
      if (newVal === 'tale') this.startAutoScroll();
      else this.stopAutoScroll();
    }
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Bangers&family=Oswald:wght@300;500;700&family=Luckiest+Guy&display=swap');

* { margin: 0; padding: 0; box-sizing: border-box; }
body { background-color: #000; overflow: hidden; font-family: 'Oswald', sans-serif; color: white; }

/* BG ENGINE */
.bg-container { position: fixed; top: 0; left: 0; width: 100vw; height: 100vh; z-index: -2; }
.bg-layer { position: absolute; top: 0; left: 0; width: 100%; height: 100%; object-fit: cover; opacity: 0; transition: opacity 1.2s ease-in-out; }
.bg-layer.visible { opacity: 1; }
.overlay { position: absolute; top: 0; left: 0; width: 100%; height: 100%; z-index: -1; transition: 1.5s ease; }
.overlay.menu-active { background: rgba(0, 0, 0, 0.4); }

/* LOADING SCREEN OVERRIDES */
/* ADDED NULLIFY STYLES */
.nullify-text { font-family: 'Bangers'; color: #f4d03f; font-size: 3.5rem; letter-spacing: 2px; margin-bottom: 20px; text-shadow: 2px 2px 10px black; }
.nullify-gif { width: 100% !important; height: 100% !important; object-fit: cover !important; }

/* CAPTAIN'S TALE UPDATES */
/* ADDED LARGER TITLE IMAGE STYLE */
.tale-title-img-large { width: 480px; margin-bottom: 30px; filter: drop-shadow(0 0 15px #f4d03f); }
.tale-screen { position: absolute; top: 0; left: 0; width: 100vw; height: 100vh; display: flex; justify-content: center; align-items: center; z-index: 50; padding: 40px; }
.tale-container { display: flex; width: 90%; max-width: 1300px; height: 85vh; background: rgba(0, 0, 0, 0.85); border: 3px solid #f4d03f; backdrop-filter: blur(10px); padding: 40px; border-radius: 10px; gap: 40px; }
.tale-content { flex: 1.2; display: flex; flex-direction: column; }
.tale-scroll { overflow-y: auto; padding-right: 20px; font-size: 1.15rem; line-height: 1.6; font-weight: 300; }
.mission-text { border-left: 4px solid #f4d03f; padding-left: 15px; color: #f4d03f; font-style: italic; margin: 20px 0; }

/* MAIN MENU UPDATES */
/* ADDED MENU WRAPPER AND TITLE STYLE */
.menu-wrapper { display: flex; flex-direction: column; align-items: flex-start; gap: 20px; }
.menu-main-title { font-family: 'Bangers'; font-size: 2.2rem; color: #f4d03f; text-shadow: 3px 3px 0px black; letter-spacing: 1.5px; }

/* GLOBAL UI Elements */
.main-logo { position: fixed; top: 20px; left: 20px; width: 60px; z-index: 150; cursor: pointer; filter: drop-shadow(0 0 10px #f4d03f); }
.stage { display: flex; width: 200vw; height: 100vh; transition: 1.2s cubic-bezier(0.85, 0, 0.15, 1); }
.is-shifted { transform: translateX(-100vw); }
.screen { width: 100vw; height: 100vh; display: flex; align-items: center; padding-left: 8%; }
.loading-overlay { position: fixed; top: 0; left: 0; width: 100vw; height: 100vh; background: black; z-index: 200; display: flex; flex-direction: column; justify-content: center; align-items: center; }
.scam-text { color: #ff0000; font-family: 'Bangers'; font-size: 5rem; animation: shake 0.1s infinite; }
.trap-view { position: absolute; top: 0; left: 0; width: 100vw; height: 100vh; display: flex; flex-direction: column; justify-content: center; align-items: center; z-index: 10; }
.trap-title { font-size: 4rem; font-family: 'Luckiest Guy'; text-shadow: 4px 4px 0px #ff0000; }
.devil-fruit { width: 200px; animation: float 3s ease-in-out infinite; }
.eat-btn { margin-top: 20px; background: #f4d03f; border: 4px solid #5d4037; font-family: 'Bangers'; font-size: 2rem; padding: 10px 30px; cursor: pointer; }
.menu-screen-final { position: absolute; top: 0; right: 0; width: 100vw; height: 100vh; display: flex; justify-content: flex-end; align-items: center; padding-right: 5%; }
.stacked-nav { display: flex; flex-direction: column; gap: 15px; }
.menu-item-stack { background: rgba(0, 0, 0, 0.7); border-left: 5px solid #f4d03f; color: white; font-family: 'Oswald'; font-size: 1.1rem; font-weight: bold; padding: 15px 30px; width: 280px; text-align: left; cursor: pointer; transition: 0.3s; }
.menu-item-stack:hover { background: #f4d03f; color: black; transform: translateX(-10px); }
.carousel-frame { width: 100%; height: 100%; border: 10px solid #2c1a11; position: relative; display: flex; flex-direction: column; }
.carousel-img { width: 100%; height: 100%; object-fit: cover; }
.carousel-controls { display: flex; justify-content: space-between; align-items: center; background: #2c1a11; padding: 10px; color: #f4d03f; font-family: 'Bangers'; }
.lightbox { position: fixed; top: 0; left: 0; width: 100vw; height: 100vh; background: rgba(0,0,0,0.9); z-index: 1000; display: flex; justify-content: center; align-items: center; }
.lightbox-content { max-height: 85vh; border: 5px solid white; }

@keyframes shake { 0% { transform: translate(1px, 1px); } 50% { transform: translate(-2px, -1px); } 100% { transform: translate(1px, -2px); } }
@keyframes float { 0%, 100% { transform: translateY(0); } 50% { transform: translateY(-20px); } }
.anim-float { animation: float 3s ease-in-out infinite; }
.fade-enter-active, .fade-leave-active { transition: opacity 0.5s; }
.fade-enter-from, .fade-leave-to { opacity: 0; }
</style>