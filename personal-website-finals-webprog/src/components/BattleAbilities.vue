<template>
  <div class="battle-screen">
    <div class="battle-container">
      <div class="header-area">
        <button @click="$emit('close')" class="back-to-deck">← Return to Captain's Deck</button>
        <h1 class="battle-title">🗡️ BATTLE ABILITIES</h1>
        <p class="subtitle">The weapons and tactics used to conquer the digital Grand Line.</p>
      </div>

      <div class="abilities-grid">
        <div v-for="(skill, index) in skills" :key="index" class="ability-card">
          <div class="card-visual">
            <img :src="skill.image" :alt="skill.title" class="skill-img" />
            <div class="ability-tag">{{ skill.category }}</div>
          </div>
          <div class="ability-info">
            <h3>{{ skill.icon }} {{ skill.title }}</h3>
            <p>{{ skill.description }}</p>
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
      skills: [
        {
          title: "Video Editing",
          category: "CREATIVE",
          icon: "🎬",
          image: "https://images.unsplash.com/photo-1574717024653-61fd2cf4d44d?q=80&w=500",
          description: "Not just cutting clips — I craft stories. From timing transitions to syncing music and visuals, I know how to turn raw footage into engaging content."
        },
        {
          title: "Basic Programming",
          category: "TECHNICAL",
          icon: "💻",
          image: "https://images.unsplash.com/photo-1461749280684-dccba630e2f6?q=80&w=500",
          description: "Trained in HTML, CSS, JavaScript, and backend basics. I understand logic, conditions, loops, APIs, and system structure."
        },
        {
          title: "Communication",
          category: "LEADERSHIP",
          icon: "🗣️",
          // LINK FIXED BELOW
          image: "https://raw.githubusercontent.com/ushmaryosep/personal-website-finals-webprog/main/assets(gif%2C%20png%2C%20jpg)/communication.png",
          description: "A captain must speak clearly. I can present ideas confidently, explain technical concepts simply, and collaborate effectively with teammates."
        },
        {
          title: "Problem Solving",
          category: "TACTICAL",
          icon: "🧠",
          image: "https://images.unsplash.com/photo-1516062423079-7ca13cdc7f5a?q=80&w=500",
          description: "I stay calm under pressure and break problems down logically. I analyze, test, and improve — treating every challenge as a puzzle."
        },
        {
          title: "Adaptability",
          category: "GROWTH",
          icon: "🚀",
          image: "https://images.unsplash.com/photo-1519389950473-47ba0277781c?q=80&w=500",
          description: "The tech world changes fast — and I adapt faster. I believe growth is non-negotiable, adding another weapon to my arsenal constantly."
        }
      ]
    }
  }
}
</script>

<style scoped>
.battle-screen {
  position: fixed; 
  top: 0; 
  left: 0; 
  width: 100vw; 
  height: 100vh;
  background: linear-gradient(rgba(0,0,0,0.85), rgba(0,0,0,0.95)), 
              /* LINK FIXED BELOW */
              url('https://raw.githubusercontent.com/ushmaryosep/personal-website-finals-webprog/main/assets(gif%2C%20png%2C%20jpg)/BG%203.gif');
  background-size: cover; 
  z-index: 100; 
  overflow-y: auto; 
  color: white;

  &::-webkit-scrollbar {
    display: none;
  }
  -ms-overflow-style: none;  
  scrollbar-width: none;  
}

.battle-container { max-width: 1200px; margin: 0 auto; padding: 60px 20px; }

.header-area { text-align: center; margin-bottom: 50px; }
.back-to-deck { 
  background: none; 
  border: 1px solid #f4d03f; 
  color: #f4d03f; 
  padding: 8px 20px; 
  cursor: pointer; 
  margin-bottom: 20px; 
  font-family: 'Oswald'; 
}
.battle-title { font-family: 'Bangers'; font-size: 4.5rem; color: #f4d03f; text-shadow: 4px 4px 0px #000; }
.subtitle { font-size: 1.2rem; color: #ccc; font-style: italic; }

.abilities-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(350px, 1fr));
  gap: 30px;
}

.ability-card {
  background: rgba(20, 20, 20, 0.8);
  border: 1px solid #333;
  border-radius: 12px;
  overflow: hidden;
  transition: transform 0.3s ease, border-color 0.3s ease;
}

.ability-card:hover {
  transform: translateY(-10px);
  border-color: #f4d03f;
}

.card-visual {
  height: 200px;
  position: relative;
}

.skill-img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  filter: grayscale(40%);
}

.ability-tag {
  position: absolute;
  top: 15px;
  right: 15px;
  background: #f4d03f;
  color: black;
  font-family: 'Bangers';
  padding: 4px 12px;
  border-radius: 4px;
  font-size: 0.9rem;
}

.ability-info {
  padding: 25px;
}

.ability-info h3 {
  font-family: 'Bangers';
  font-size: 1.8rem;
  color: #f4d03f;
  margin-bottom: 15px;
  letter-spacing: 1px;
}

.ability-info p {
  color: #ddd;
  line-height: 1.6;
  font-size: 1.05rem;
  font-weight: 300;
}
</style>