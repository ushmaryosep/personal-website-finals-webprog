<template>
  <div class="training-screen">
    <div class="training-scroll-area">
      <h1 class="training-title">📜 Grand Line Training</h1>
      <p class="training-intro">Every great pirate captain was once a cabin boy. Before conquering the seas of technology, I trained across different islands of knowledge, sharpening my mind and preparing for the digital Grand Line.</p>
      <div class="training-timeline">
        <div class="training-node">
          <div class="node-header">
            <img src="https://github.com/ushmaryosep/personal-website-finals-webprog/blob/main/assets(gif%2C%20png%2C%20jpg)/hslbclogo%20(2).png" class="school-logo" />
            <h2 class="node-title">⚓ Elementary Voyage (2010 – 2017)</h2>
          </div>
          <p class="node-school">HSL – Braille College, Inc.</p>
          <p class="node-addr">26C Durian Ext., Pag-Asa Ave., Brgy. Katuparan, Taguig City</p>
          <p class="node-text">This was where the foundation of my journey began — learning discipline, curiosity, and the courage to explore beyond the horizon.</p>
        </div>
        <div class="training-node">
          <div class="node-header">
            <img src="https://github.com/ushmaryosep/personal-website-finals-webprog/blob/main/assets(gif%2C%20png%2C%20jpg)/hslbclogo%20(2).png" class="school-logo" />
            <h2 class="node-title">⚓ Junior High Expedition (2017 – 2022)</h2>
          </div>
          <p class="node-school">HSL – Braille College, Inc.</p>
          <p class="node-addr">26C Durian Ext., Pag-Asa Ave., Brgy. Katuparan, Taguig City</p>
          <p class="node-text">Here, I strengthened my skills, built resilience, and discovered my growing interest in technology and problem-solving.</p>
        </div>
        <div class="training-node">
          <div class="node-header">
            <img src="https://github.com/ushmaryosep/personal-website-finals-webprog/blob/main/assets(gif%2C%20png%2C%20jpg)/hslbclogo%20(2).png" class="school-logo" />
            <h2 class="node-title">⚓ Senior High Specialization (2022 – 2024)</h2>
          </div>
          <p class="node-school">HSL – Braille College, Inc.</p>
          <p class="node-addr">26C Durian Ext., Pag-Asa Ave., Brgy. Katuparan, Taguig City</p>
          <p class="node-text">The years that shaped my direction — where ambition met clarity, and I chose to sail toward the world of Information Technology.</p>
          <img src="https://github.com/ushmaryosep/personal-website-finals-webprog/blob/main/assets(gif%2C%20png%2C%20jpg)/hslbcpic1.png" class="expedition-pic" />
        </div>
        <div class="training-node active-voyage">
          <div class="node-header">
            <img src="https://github.com/ushmaryosep/personal-website-finals-webprog/blob/main/assets(gif%2C%20png%2C%20jpg)/apclogo.png" class="school-logo" />
            <h2 class="node-title">🏴‍☠️ College – The Grand Line (2024 – 2028)</h2>
          </div>
          <p class="node-school gold-text">Asia Pacific College</p>
          <p class="node-addr">3 Humabon Place, Magallanes, Makati City 1232 PH</p>
          <p class="node-text">Currently sailing as a second-year Information Technology student, mastering the arts of coding, systems, and digital innovation — preparing to command my own fleet in the future.</p>
          <img src="https://github.com/ushmaryosep/personal-website-finals-webprog/blob/main/assets(gif%2C%20png%2C%20jpg)/apcpic1.png" />
        </div>
      </div>
      <button @click="$emit('close')" class="back-to-menu-training">← BACK TO Captain's Deck</button>
    </div>
  </div>
</template>

<style scoped>
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
</style>