<template>
  <div id="app" class="grand-line">
    
    <div class="bg-container">
      <img 
        src="https://github.com/ushmaryosep/personal-website-finals/blob/main/live%20background.gif?raw=true" 
        class="bg-layer" :class="{ 'visible': currentView === 'main' }"
      />
      <img 
        src="https://github.com/ushmaryosep/personal-website-finals-webprog/blob/main/bg2.gif?raw=true" 
        class="bg-layer" :class="{ 'visible': currentView === 'trap' }"
      />
      <img 
        src="https://github.com/ushmaryosep/personal-website-finals-webprog/blob/main/main%20menu.gif?raw=true" 
        class="bg-layer" :class="{ 'visible': currentView === 'menu' }"
      />
      <img 
        src="https://github.com/ushmaryosep/personal-website-finals-webprog/blob/main/BG%203.gif?raw=true" 
        class="bg-layer" :class="{ 'visible': currentView === 'tale' || currentView === 'training' || currentView === 'hobbies' }"
      />
    </div>

    <div class="overlay" :class="{ 
      'trap-active': currentView === 'trap', 
      'menu-active': currentView === 'menu' || currentView === 'tale' || currentView === 'training' || currentView === 'hobbies'
    }"></div>

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
        <template v-if="!isNullifying">
          <h1 class="scam-text">YOU'VE BEEN SCAMMED!</h1>
          <img src="https://github.com/ushmaryosep/personal-website-finals-webprog/blob/main/loading%20screen.gif?raw=true" alt="Loading..." />
        </template>
        <template v-else>
          <h1 class="nullify-text">EFFECTS NOW NULLIFYING...</h1>
          <img src="https://github.com/ushmaryosep/personal-website-finals-webprog/blob/main/nullifying%20effects.gif?raw=true" class="nullify-bg" />
        </template>
      </div>
    </transition>

    <div v-if="currentView === 'main'" class="stage" :class="{ 'is-shifted': showPoster }">
      
      <section class="screen section-left">
        <div class="content-box left-aligned">
          <img 
            src="https://raw.githubusercontent.com/ushmaryosep/personal-website-finals/refs/heads/main/hero%20title.png" 
            class="hero-title-img"
          />
          <p class="pirate-description">
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
        
        <div class="fruit-container" @click="triggerNullifying">
          <img 
            src="https://github.com/ushmaryosep/personal-website-finals-webprog/blob/main/FRUIT.png?raw=true" 
            class="devil-fruit" 
          />
          <button class="eat-btn">EAT THIS 🍎</button>
        </div>
      </div>
    </transition>

    <transition name="fade">
      <div v-if="currentView === 'training'" class="training-screen">
        <div class="training-scroll-area">
          <h1 class="training-title">📜 Grand Line Training</h1>
          <p class="training-intro">Every great pirate captain was once a cabin boy. Before conquering the seas of technology, I trained across different islands of knowledge, sharpening my mind and preparing for the digital Grand Line.</p>
          
          <div class="training-timeline">
            <div class="training-node">
              <div class="node-header">
                <img src="https://github.com/ushmaryosep/personal-website-finals-webprog/blob/main/hslbclogo%20(2).png?raw=true" class="school-logo" />
                <h2 class="node-title">⚓ Elementary Voyage (2010 – 2017)</h2>
              </div>
              <p class="node-school">HSL – Braille College, Inc.</p>
              <p class="node-addr">26C Durian Ext., Pag-Asa Ave., Brgy. Katuparan, Taguig City</p>
              <p class="node-text">This was where the foundation of my journey began — learning discipline, curiosity, and the courage to explore beyond the horizon.</p>
            </div>

            <div class="training-node">
              <div class="node-header">
                <img src="https://github.com/ushmaryosep/personal-website-finals-webprog/blob/main/hslbclogo%20(2).png?raw=true" class="school-logo" />
                <h2 class="node-title">⚓ Junior High Expedition (2017 – 2022)</h2>
              </div>
              <p class="node-school">HSL – Braille College, Inc.</p>
              <p class="node-addr">26C Durian Ext., Pag-Asa Ave., Brgy. Katuparan, Taguig City</p>
              <p class="node-text">Here, I strengthened my skills, built resilience, and discovered my growing interest in technology and problem-solving.</p>
            </div>

            <div class="training-node">
              <div class="node-header">
                <img src="https://github.com/ushmaryosep/personal-website-finals-webprog/blob/main/hslbclogo%20(2).png?raw=true" class="school-logo" />
                <h2 class="node-title">⚓ Senior High Specialization (2022 – 2024)</h2>
              </div>
              <p class="node-school">HSL – Braille College, Inc.</p>
              <p class="node-addr">26C Durian Ext., Pag-Asa Ave., Brgy. Katuparan, Taguig City</p>
              <p class="node-text">The years that shaped my direction — where ambition met clarity, and I chose to sail toward the world of Information Technology.</p>
              <img src="https://github.com/ushmaryosep/personal-website-finals-webprog/blob/main/hslbcpic1.png?raw=true" class="expedition-pic" />
            </div>

            <div class="training-node active-voyage">
              <div class="node-header">
                <img src="https://github.com/ushmaryosep/personal-website-finals-webprog/blob/main/apclogo.png?raw=true" class="school-logo" />
                <h2 class="node-title">🏴‍☠️ College – The Grand Line (2024 – 2028)</h2>
              </div>
              <p class="node-school gold-text">Asia Pacific College</p>
              <p class="node-addr">3 Humabon Place, Magallanes, Makati City 1232 PH</p>
              <p class="node-text">Currently sailing as a second-year Information Technology student, mastering the arts of coding, systems, and digital innovation — preparing to command my own fleet in the future.</p>
              <img src="https://github.com/ushmaryosep/personal-website-finals-webprog/blob/main/apcpic1.png?raw=true" class="expedition-pic" />
            </div>
          </div>
          <button @click="currentView = 'menu'" class="back-to-menu-training">← BACK TO NAV NAVI</button>
        </div>
      </div>
    </transition>

    <transition name="fade">
      <div v-if="currentView === 'tale'" class="tale-screen">
        <div class="tale-container">
          <div class="tale-content">
            <img src="https://github.com/ushmaryosep/personal-website-finals-webprog/blob/main/captain's%20tale.png?raw=true" class="tale-title-img-big anim-float" />
            <div class="tale-scroll">
              <p>Ahoy. I be <strong>Joshmar Clavero</strong>, a second-year Information Technology cadet sailing under the banner of Asia Pacific College. From a young age, I found myself drawn to the world of machines, systems, and the endless ocean of technology — a realm where logic commands power and creativity shapes reality.</p>
              <p>My passion lies in all things computers — from coding and system building to understanding how technology shapes modern society. I chose the path of IT not merely for a degree, but for mastery. In this ever-evolving digital Grand Line, I aim to sharpen my skills, expand my knowledge, and become a captain worthy of leading my own fleet of innovations.</p>
              <p class="mission-text">
                Beyond ambition, I carry a deeper mission: To rise, to build wealth, and to become a billionaire — not for glory alone, but to secure the future of my parents and siblings. Every project I complete, every skill I train, and every challenge I overcome brings me one step closer to that dream.
              </p>
              <p>I believe technology is power — and power, when guided by purpose, can change lives. This is only the beginning of my voyage.</p>
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
      <CrewPastimes v-if="currentView === 'hobbies'" @close="currentView = 'menu'" />
    </transition>

    <transition name="fade">
      <div v-if="currentView === 'menu'" class="menu-screen-final">
        <div class="menu-nav-container">
          <h1 class="menu-header">WELCOME TO THE CAPTAIN'S DECK</h1>
          <div class="stacked-nav">
            <button class="menu-item-stack" @click="currentView = 'tale'">⚓ The Captain’s Tale</button>
            <button class="menu-item-stack" @click="currentView = 'training'">📜 Grand Line Training</button>
            <button class="menu-item-stack" @click="currentView = 'hobbies'">🍖 Crew Pastimes</button>
            <button class="menu-item-stack">🗡️ Battle Abilities</button>
            <button class="menu-item-stack">🏆 Bounties & Glory</button>
            <button class="menu-item-stack">🕊️ Send a Message</button>
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

export default {
  name: 'App',
  components: {
    CrewPastimes
  },
  data() {
    return {
      showPoster: false,
      isLoading: false,
      isNullifying: false,
      currentView: 'main',
      currentImgIndex: 0,
      isLightboxOpen: false,
      carouselTimer: null,
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
    triggerTrap() {
      this.isNullifying = false;
      this.isLoading = true;
      setTimeout(() => {
        this.isLoading = false;
        this.currentView = 'trap';
      }, 2200);
    },
    triggerNullifying() {
      this.isNullifying = true;
      this.isLoading = true;
      setTimeout(() => {
        this.isLoading = false;
        this.currentView = 'menu';
      }, 3000);
    },
    resetToHome() {
      this.currentView = 'main';
      this.showPoster = false;
    },
    nextImg() {
      this.currentImgIndex = (this.currentImgIndex + 1) % this.carouselImages.length;
    },
    prevImg() {
      this.currentImgIndex = (this.currentImgIndex - 1 + this.carouselImages.length) % this.carouselImages.length;
    }
  },
  watch: {
    currentView(newVal) {
      if (newVal === 'tale') {
        this.carouselTimer = setInterval(() => {
          this.nextImg();
        }, 3000);
      } else {
        clearInterval(this.carouselTimer);
      }
    }
  }
}
</script>

<style>
/* 1. SCROLLBAR SUPPRESSION (GLOBAL) */
* { 
  margin: 0; padding: 0; box-sizing: border-box; 
  /* Hide scrollbar for Chrome, Safari and Opera */
  &::-webkit-scrollbar { display: none; }
  /* Hide scrollbar for IE, Edge and Firefox */
  -ms-overflow-style: none;  /* IE and Edge */
  scrollbar-width: none;  /* Firefox */
}

/* 2. FONTS */
@import url('https://fonts.googleapis.com/css2?family=Bangers&family=Oswald:wght@300;500;700&family=Luckiest+Guy&display=swap');

body { background-color: #000; overflow: hidden; font-family: 'Oswald', sans-serif; color: white; }

/* 3. BACKGROUND ENGINE */
.bg-container {
  position: fixed; top: 0; left: 0; width: 100vw; height: 100vh; z-index: -2;
}
.bg-layer {
  position: absolute; top: 0; left: 0; width: 100%; height: 100%;
  object-fit: cover; opacity: 0; transition: opacity 1.2s ease-in-out;
}
.bg-layer.visible { opacity: 1; }

.overlay {
  position: absolute; top: 0; left: 0; width: 100%; height: 100%;
  z-index: -1; transition: 1.5s ease;
}
.overlay.trap-active { background: rgba(0, 0, 0, 0.75); }
.overlay.menu-active { background: rgba(0, 0, 0, 0.6); }

/* 4. CAPTAIN'S TALE STYLING */
.tale-screen {
  position: absolute; top: 0; left: 0; width: 100vw; height: 100vh;
  display: flex; justify-content: center; align-items: center; z-index: 50; padding: 40px;
}
.tale-container {
  display: flex; width: 90%; max-width: 1200px; height: 80vh;
  background: rgba(0, 0, 0, 0.85); border: 3px solid #f4d03f;
  backdrop-filter: blur(10px); padding: 40px; border-radius: 10px; gap: 40px;
}
.tale-content { flex: 1.2; display: flex; flex-direction: column; text-align: left; }
.tale-title-img-big { width: 450px; margin-bottom: 20px; }
.tale-scroll { 
  overflow-y: auto; padding-right: 5px; font-size: 1.1rem; 
  line-height: 1.6; font-weight: 300; color: #ddd; 
}
.tale-scroll p { margin-bottom: 20px; }
.mission-text { border-left: 4px solid #f4d03f; padding-left: 15px; color: #f4d03f; font-style: italic; }
.back-to-menu { 
  margin-top: auto; background: none; border: 1px solid #f4d03f; 
  color: #f4d03f; padding: 10px 20px; cursor: pointer; width: fit-content;
}

/* 5. TRAINING SCREEN STYLING (LOGOS & IMAGES ADDED) */
.training-screen {
  position: absolute; top: 0; left: 0; width: 100vw; height: 100vh;
  display: flex; justify-content: center; align-items: center; z-index: 55;
  padding: 60px 20px;
}
.training-scroll-area {
  max-width: 900px; width: 100%; height: 90vh; overflow-y: auto;
  padding-right: 5px;
}
.training-title { font-family: 'Bangers'; font-size: 4rem; color: #f4d03f; margin-bottom: 10px; text-shadow: 4px 4px 0px #000; }
.training-intro { font-size: 1.3rem; line-height: 1.5; color: #ccc; margin-bottom: 40px; }
.training-timeline { display: flex; flex-direction: column; gap: 40px; }
.training-node { border-left: 2px solid #f4d03f; padding-left: 30px; position: relative; padding-bottom: 30px; }

.node-header { display: flex; align-items: center; gap: 15px; margin-bottom: 10px; }
.school-logo { width: 50px; height: 50px; object-fit: contain; filter: drop-shadow(0 0 5px rgba(244, 208, 63, 0.4)); }
.expedition-pic { margin-top: 20px; width: 100%; max-width: 500px; border: 4px solid #2c1a11; border-radius: 5px; box-shadow: 0 10px 20px rgba(0,0,0,0.5); }

.node-title { font-family: 'Bangers'; color: #f4d03f; font-size: 1.8rem; letter-spacing: 1px; }
.node-school { font-weight: bold; font-size: 1.2rem; color: #fff; margin: 5px 0; }
.node-addr { font-size: 0.9rem; color: #888; font-style: italic; margin-bottom: 10px; }
.node-text { color: #ddd; line-height: 1.6; }
.gold-text { color: #f4d03f !important; text-transform: uppercase; }
.back-to-menu-training { 
  margin-top: 50px; background: none; border: 2px solid #f4d03f; 
  color: #f4d03f; padding: 12px 30px; font-family: 'Bangers'; 
  font-size: 1.5rem; cursor: pointer; transition: 0.3s;
}
.back-to-menu-training:hover { background: #f4d03f; color: #000; }

/* 6. CAROUSEL STYLING */
.carousel-section { flex: 0.8; display: flex; justify-content: center; align-items: center; }
.carousel-frame {
  width: 100%; height: 100%; border: 10px solid #2c1a11; 
  position: relative; box-shadow: 0 0 20px rgba(0,0,0,0.5);
  display: flex; flex-direction: column;
}
.carousel-img { width: 100%; height: 100%; object-fit: cover; cursor: pointer; transition: 0.3s; }
.carousel-controls {
  display: flex; justify-content: space-between; align-items: center;
  background: #2c1a11; padding: 10px; color: #f4d03f; font-family: 'Bangers';
}
.carousel-controls button { background: none; border: none; color: #f4d03f; cursor: pointer; font-size: 1.5rem; }

/* 7. MENU STACKED */
.menu-screen-final {
  position: absolute; top: 0; right: 0; width: 100vw; height: 100vh;
  display: flex; justify-content: flex-end; align-items: center; padding-right: 5%;
}
.menu-nav-container { display: flex; flex-direction: column; align-items: flex-start; gap: 20px; }
.menu-header { font-family: 'Bangers'; color: #f4d03f; font-size: 2.5rem; text-shadow: 3px 3px 0px #000; }
.stacked-nav { display: flex; flex-direction: column; gap: 15px; }
.menu-item-stack {
  background: rgba(0, 0, 0, 0.7); border-left: 5px solid #f4d03f;
  color: white; font-family: 'Oswald'; font-size: 1.1rem; font-weight: bold;
  padding: 15px 30px; width: 250px; text-align: left; cursor: pointer;
  transition: 0.3s; backdrop-filter: blur(5px);
}
.menu-item-stack:hover { background: #f4d03f; color: black; transform: translateX(-10px); }

/* 8. GLOBAL COMPONENTS */
.main-logo { position: fixed; top: 20px; left: 20px; width: 60px; z-index: 150; cursor: pointer; filter: drop-shadow(0 0 10px #f4d03f); }
.stage { display: flex; width: 200vw; height: 100vh; transition: 1.2s cubic-bezier(0.85, 0, 0.15, 1); }
.is-shifted { transform: translateX(-100vw); }
.screen { width: 100vw; height: 100vh; display: flex; align-items: center; padding-left: 8%; }

.loading-overlay {
  position: fixed; top: 0; left: 0; width: 100vw; height: 100vh;
  background: black; z-index: 200; display: flex; flex-direction: column;
  justify-content: center; align-items: center;
}
.scam-text { color: #ff0000; font-family: 'Bangers'; font-size: 5rem; animation: shake 0.1s infinite; }
.nullify-text { color: #f4d03f; font-family: 'Bangers'; font-size: 4rem; z-index: 10; text-shadow: 4px 4px 0px #000; }
.nullify-bg { position: absolute; width: 100%; height: 100%; object-fit: cover; z-index: 5; }

.trap-view {
  position: absolute; top: 0; left: 0; width: 100vw; height: 100vh;
  display: flex; flex-direction: column; justify-content: center; align-items: center; z-index: 10;
}
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

.lightbox {
  position: fixed; top: 0; left: 0; width: 100vw; height: 100vh;
  background: rgba(0,0,0,0.9); z-index: 1000; display: flex; 
  flex-direction: column; justify-content: center; align-items: center;
}
.lightbox-content { max-height: 85vh; max-width: 85vw; border: 5px solid white; }
.close-hint { margin-top: 20px; color: #f4d03f; font-family: 'Bangers'; letter-spacing: 2px; }

/* ANIMATIONS */
@keyframes shake { 0% { transform: translate(1px, 1px); } 50% { transform: translate(-2px, -1px); } 100% { transform: translate(1px, -2px); } }
@keyframes float { 0%, 100% { transform: translateY(0); } 50% { transform: translateY(-20px); } }
@keyframes titleZoom { 0%, 100% { transform: scale(1); } 50% { transform: scale(1.03); } }
.anim-float { animation: float 3s ease-in-out infinite; }

.fade-enter-active, .fade-leave-active { transition: opacity 0.5s; }
.fade-enter-from, .fade-leave-to { opacity: 0; }
.zoom-in-enter-active { transition: all 0.8s cubic-bezier(0.34, 1.56, 0.64, 1); }
.zoom-in-enter-from { opacity: 0; transform: scale(1.2); }
</style>