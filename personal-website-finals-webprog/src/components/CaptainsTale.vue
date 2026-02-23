<template>
  <div class="tale-screen">
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
        <button @click="$emit('close')" class="back-to-menu">← BACK TO Captain's Deck</button>
      </div>

      <div class="carousel-section">
        <div class="carousel-frame">
          <transition name="fade" mode="out-in">
            <img :src="carouselImages[currentImgIndex]" :key="currentImgIndex" class="carousel-img" @click="$emit('open-lightbox', currentImgIndex)" />
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
</template>

<script>
export default {
  props: ['carouselImages', 'currentImgIndex'],
  methods: {
    nextImg() { this.$emit('next'); },
    prevImg() { this.$emit('prev'); }
  }
}
</script>

<style scoped>
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
.anim-float { animation: float 3s ease-in-out infinite; }
@keyframes float { 0%, 100% { transform: translateY(0); } 50% { transform: translateY(-20px); } }
</style>