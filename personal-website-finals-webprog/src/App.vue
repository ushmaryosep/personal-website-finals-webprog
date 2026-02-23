<template>
  <div id="app" class="grand-line">
    
    <div class="bg-container">
      <img src="https://github.com/ushmaryosep/personal-website-finals/blob/main/live%20background.gif?raw=true" class="bg-layer" :class="{ 'visible': currentView === 'main' }"/>
      <img src="https://github.com/ushmaryosep/personal-website-finals-webprog/blob/main/assets(gif%2C%20png%2C%20jpg)/bg2.gif" class="bg-layer" :class="{ 'visible': currentView === 'trap' }"/>
      <img src="https://github.com/ushmaryosep/personal-website-finals-webprog/blob/main/assets(gif%2C%20png%2C%20jpg)/main%20menu.gif" class="bg-layer" :class="{ 'visible': currentView === 'menu' }"/>
      <img src="https://github.com/ushmaryosep/personal-website-finals-webprog/blob/main/assets(gif%2C%20png%2C%20jpg)/BG%203.gif" class="bg-layer" :class="{ 'visible': ['tale', 'training', 'hobbies', 'battle', 'soundtrack'].includes(currentView) }"/>
      <img src="https://github.com/ushmaryosep/personal-website-finals-webprog/blob/main/assets(gif%2C%20png%2C%20jpg)/final%20bg.gif" class="bg-layer" :class="{ 'visible': currentView === 'messenger' }"/>
    </div>

    <div class="overlay" :class="{ 'trap-active': currentView === 'trap', 'menu-active': ['menu', 'tale', 'training', 'hobbies', 'battle', 'soundtrack', 'messenger'].includes(currentView) }"></div>

    <transition name="fade">
      <img v-if="showPoster || currentView !== 'main'" src="https://github.com/ushmaryosep/personal-website-finals-webprog/blob/main/assets(gif%2C%20png%2C%20jpg)/mylogo.png" class="main-logo" @click="resetToHome" alt="Logo"/>
    </transition>

    <transition name="fade">
      <div v-if="isLoading" class="loading-overlay">
        <template v-if="!isNullifying">
          <h1 class="scam-text">YOU'VE BEEN SCAMMED!</h1>
          <img src="https://github.com/ushmaryosep/personal-website-finals-webprog/blob/main/assets(gif%2C%20png%2C%20jpg)/loading%20screen.gif" alt="Loading..." />
        </template>
        <template v-else>
          <h1 class="nullify-text">EFFECTS NOW NULLIFYING...</h1>
          <img src="https://github.com/ushmaryosep/personal-website-finals-webprog/blob/main/assets(gif%2C%20png%2C%20jpg)/nullifying%20effects.gif" class="nullify-bg" />
        </template>
      </div>
    </transition>

    <div v-if="currentView === 'main'" class="stage" :class="{ 'is-shifted': showPoster }">
      <section class="screen section-left">
        <div class="content-box left-aligned">
          <img src="https://raw.githubusercontent.com/ushmaryosep/personal-website-finals/refs/heads/main/hero%20title.png" class="hero-title-img"/>
          <p class="pirate-description">Ahoy, wanderer of the seas! This be the personal stronghold of Joshmar Clavero. Within these coordinates, you’ll find the chronicles of a developer-pirate: from the grueling logs of Grand Line Training to the ultimate Battle Abilities. Explore the deck, but heed the warning—the Marines are always watching, and not every fruit you find is sweet.</p>
          <button @click="showPoster = true" class="pirate-btn">VIEW WANTED POSTER ☠</button>
        </div>
      </section>

      <section class="screen section-right">
        <div class="poster-wrap left-aligned-poster">
          <img src="https://raw.githubusercontent.com/ushmaryosep/personal-website-finals/refs/heads/main/HERO%20CARD.png" class="wanted-card"/>
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
        <div class="fruit-container" @click="triggerNullifying">
          <img src="https://github.com/ushmaryosep/personal-website-finals-webprog/blob/main/assets(gif%2C%20png%2C%20jpg)/FRUIT.png" class="devil-fruit" />
          <button class="eat-btn">EAT THIS 🍎</button>
        </div>
      </div>
    </transition>

    <transition name="fade">
      <GrandLineTraining v-if="currentView === 'training'" @close="currentView = 'menu'" />
    </transition>

    <transition name="fade">
      <CaptainsTale 
        v-if="currentView === 'tale'" 
        :carouselImages="carouselImages" 
        :currentImgIndex="currentImgIndex"
        @next="nextImg" @prev="prevImg"
        @close="currentView = 'menu'" 
        @open-lightbox="(idx) => { currentImgIndex = idx; isLightboxOpen = true; }" 
      />
    </transition>

    <transition name="fade">
      <CrewPastimes v-if="currentView === 'hobbies'" @close="currentView = 'menu'" />
    </transition>

    <transition name="fade">
      <BattleAbilities v-if="currentView === 'battle'" @close="currentView = 'menu'" />
    </transition>

    <transition name="fade">
      <CaptainsSoundtrack v-if="currentView === 'soundtrack'" @close="currentView = 'menu'" />
    </transition>

    <transition name="fade">
      <MessengerDeck v-if="currentView === 'messenger'" @close="currentView = 'menu'" />
    </transition>

    <transition name="fade">
      <div v-if="currentView === 'menu'" class="menu-screen-final">
        <div class="menu-nav-container">
          <h1 class="menu-header">WELCOME TO THE CAPTAIN'S DECK</h1>
          <div class="stacked-nav">
            <button class="menu-item-stack" @click="currentView = 'tale'">⚓ The Captain’s Tale</button>
            <button class="menu-item-stack" @click="currentView = 'training'">📜 Grand Line Training</button>
            <button class="menu-item-stack" @click="currentView = 'hobbies'">🍖 Crew Pastimes</button>
            <button class="menu-item-stack" @click="currentView = 'battle'">🗡️ Battle Abilities</button>
            <button class="menu-item-stack" @click="currentView = 'soundtrack'">🎶 Captain’s Soundtrack</button>
            <button class="menu-item-stack" @click="currentView = 'messenger'">🕊️ Send a Message</button>
          </div>
        </div>
      </div>
    </transition>

    <div v-if="isLightboxOpen" class="lightbox" @click="isLightboxOpen = false">
      <img :src="carouselImages[currentImgIndex]" class="lightbox-content" />
      <p class="close-hint">CLICK ANYWHERE TO CLOSE</p>
    </div>

  </div>
</template>

<script>
import CrewPastimes from './components/CrewPastimes.vue'
import BattleAbilities from './components/BattleAbilities.vue'
import CaptainsTale from './components/CaptainsTale.vue'
import GrandLineTraining from './components/GrandLineTraining.vue'
import CaptainsSoundtrack from './components/CaptainsSoundtrack.vue'
import MessengerDeck from './components/MessengerDeck.vue'

export default {
  name: 'App',
  components: { 
    CrewPastimes, 
    BattleAbilities, 
    CaptainsTale, 
    GrandLineTraining,
    CaptainsSoundtrack,
    MessengerDeck
  },
  data() {
    return {
      showPoster: false, isLoading: false, isNullifying: false,
      currentView: 'main', currentImgIndex: 0, isLightboxOpen: false,
      carouselTimer: null,
      carouselImages: [
        'https://github.com/ushmaryosep/personal-website-finals-webprog/blob/main/assets(gif%2C%20png%2C%20jpg)/mypic1.png',
        'https://github.com/ushmaryosep/personal-website-finals-webprog/blob/main/assets(gif%2C%20png%2C%20jpg)/mypic2.png',
        'https://github.com/ushmaryosep/personal-website-finals-webprog/blob/main/assets(gif%2C%20png%2C%20jpg)/mypic3.png',
        'https://github.com/ushmaryosep/personal-website-finals-webprog/blob/main/assets(gif%2C%20png%2C%20jpg)/mypic4.png',
        'https://github.com/ushmaryosep/personal-website-finals-webprog/blob/main/assets(gif%2C%20png%2C%20jpg)/mypic5.png',
        'https://github.com/ushmaryosep/personal-website-finals-webprog/blob/main/assets(gif%2C%20png%2C%20jpg)/mypic6.png'
      ]
    }
  },
  methods: {
    triggerTrap() {
      this.isNullifying = false; this.isLoading = true;
      setTimeout(() => { this.isLoading = false; this.currentView = 'trap'; }, 2200);
    },
    triggerNullifying() {
      this.isNullifying = true; this.isLoading = true;
      setTimeout(() => { this.isLoading = false; this.currentView = 'menu'; }, 3000);
    },
    resetToHome() { this.currentView = 'main'; this.showPoster = false; },
    nextImg() { this.currentImgIndex = (this.currentImgIndex + 1) % this.carouselImages.length; },
    prevImg() { this.currentImgIndex = (this.currentImgIndex - 1 + this.carouselImages.length) % this.carouselImages.length; }
  },
  watch: {
    currentView(newVal) {
      if (newVal === 'tale') {
        this.carouselTimer = setInterval(() => { this.nextImg(); }, 3000);
      } else { clearInterval(this.carouselTimer); }
    }
  }
}
</script>

<style>
/* 1. GLOBAL STYLES */
* { 
  margin: 0; padding: 0; box-sizing: border-box; 
  &::-webkit-scrollbar { display: none; }
  -ms-overflow-style: none; scrollbar-width: none; 
}

@import url('https://fonts.googleapis.com/css2?family=Bangers&family=Oswald:wght@300;500;700&family=Luckiest+Guy&display=swap');

body { background-color: #000; overflow: hidden; font-family: 'Oswald', sans-serif; color: white; }

/* 2. BACKGROUND ENGINE */
.bg-container { position: fixed; top: 0; left: 0; width: 100vw; height: 100vh; z-index: -2; }
.bg-layer { position: absolute; top: 0; left: 0; width: 100%; height: 100%; object-fit: cover; opacity: 0; transition: opacity 1.2s ease-in-out; }
.bg-layer.visible { opacity: 1; }

.overlay { position: absolute; top: 0; left: 0; width: 100%; height: 100%; z-index: -1; transition: 1.5s ease; }
.overlay.trap-active { background: rgba(0, 0, 0, 0.75); }
.overlay.menu-active { background: rgba(0, 0, 0, 0.6); }

/* 3. MENU STACKED */
.menu-screen-final { position: absolute; top: 0; right: 0; width: 100vw; height: 100vh; display: flex; justify-content: flex-end; align-items: center; padding-right: 5%; }
.menu-nav-container { display: flex; flex-direction: column; align-items: flex-start; gap: 20px; }
.menu-header { font-family: 'Bangers'; color: #f4d03f; font-size: 2.5rem; text-shadow: 3px 3px 0px #000; }
.stacked-nav { display: flex; flex-direction: column; gap: 15px; }
.menu-item-stack { background: rgba(0, 0, 0, 0.7); border-left: 5px solid #f4d03f; color: white; font-family: 'Oswald'; font-size: 1.1rem; font-weight: bold; padding: 15px 30px; width: 250px; text-align: left; cursor: pointer; transition: 0.3s; backdrop-filter: blur(5px); }
.menu-item-stack:hover { background: #f4d03f; color: black; transform: translateX(-10px); }

/* 4. GLOBAL COMPONENTS */
.main-logo { position: fixed; top: 20px; left: 20px; width: 60px; z-index: 150; cursor: pointer; filter: drop-shadow(0 0 10px #f4d03f); }
.stage { display: flex; width: 200vw; height: 100vh; transition: 1.2s cubic-bezier(0.85, 0, 0.15, 1); }
.is-shifted { transform: translateX(-100vw); }
.screen { width: 100vw; height: 100vh; display: flex; align-items: center; padding-left: 8%; }

.loading-overlay { position: fixed; top: 0; left: 0; width: 100vw; height: 100vh; background: black; z-index: 200; display: flex; flex-direction: column; justify-content: center; align-items: center; }
.scam-text { color: #ff0000; font-family: 'Bangers'; font-size: 5rem; animation: shake 0.1s infinite; }
.nullify-text { color: #f4d03f; font-family: 'Bangers'; font-size: 4rem; z-index: 10; text-shadow: 4px 4px 0px #000; }
.nullify-bg { position: absolute; width: 100%; height: 100%; object-fit: cover; z-index: 5; }

.trap-view { position: absolute; top: 0; left: 0; width: 100vw; height: 100vh; display: flex; flex-direction: column; justify-content: center; align-items: center; z-index: 10; }
.trap-title { font-size: 4rem; font-family: 'Luckiest Guy'; text-shadow: 4px 4px 0px #ff0000; }
.red { color: #ff0000; }

.fruit-container { display: flex; flex-direction: column; align-items: center; cursor: pointer; }
.devil-fruit { width: 200px; animation: float 3s ease-in-out infinite; }
.eat-btn { margin-top: 20px; background: #f4d03f; border: 4px solid #5d4037; font-family: 'Bangers'; font-size: 2rem; padding: 10px 30px; }

.hero-title-img { width: 100%; max-width: 500px; animation: titleZoom 5s infinite; }
.pirate-description { color: white; margin: 25px 0; max-width: 480px; font-size: 1.2rem; line-height: 1.4; }
.pirate-btn { background: #f4d03f; padding: 12px 35px; border: 4px solid #5d4037; font-family: 'Bangers'; font-size: 1.5rem; cursor: pointer; }
.wanted-card { max-height: 75vh; border: 8px solid #2c1a11; }
.back-btn { background: rgba(0,0,0,0.5); color: white; border: 1px solid white; padding: 10px 20px; cursor: pointer; }
.marine-btn { background: #002d5a; color: white; border: 1px solid white; padding: 10px 20px; font-weight: bold; cursor: pointer; }
.marine-btn:hover { background: #ff0000; }

.lightbox { position: fixed; top: 0; left: 0; width: 100vw; height: 100vh; background: rgba(0,0,0,0.9); z-index: 1000; display: flex; flex-direction: column; justify-content: center; align-items: center; }
.lightbox-content { max-height: 85vh; max-width: 85vw; border: 5px solid white; }
.close-hint { margin-top: 20px; color: #f4d03f; font-family: 'Bangers'; letter-spacing: 2px; }

/* ANIMATIONS */
@keyframes shake { 0% { transform: translate(1px, 1px); } 50% { transform: translate(-2px, -1px); } 100% { transform: translate(1px, -2px); } }
@keyframes float { 0%, 100% { transform: translateY(0); } 50% { transform: translateY(-20px); } }
@keyframes titleZoom { 0%, 100% { transform: scale(1); } 50% { transform: scale(1.03); } }

.fade-enter-active, .fade-leave-active { transition: opacity 0.5s; }
.fade-enter-from, .fade-leave-to { opacity: 0; }
.zoom-in-enter-active { transition: all 0.8s cubic-bezier(0.34, 1.56, 0.64, 1); }
.zoom-in-enter-from { opacity: 0; transform: scale(1.2); }
</style>