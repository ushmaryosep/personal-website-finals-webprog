# ⚓ Captain Josh’s Personal Stronghold
**WEBPROG Finals - Personal Website Project**

Welcome to the digital Grand Line. This isn't just a portfolio; it’s a fully interactive Pirate Deck designed to showcase the journey, skills, and "wanted" status of a developer-pirate.

## 🌊 Project Summary
This website is a **Vue.js 3** Single Page Application (SPA) that creates an immersive, nautical user experience. It features a dynamic multi-view system where visitors can explore the Captain's history, training logs, and battle abilities. 

The site includes a "Pirate Trap" logic: attempting to report the Captain to the Marines triggers a "Scam" sequence that can only be nullified by consuming a Devil Fruit, which eventually grants access to the true Captain's Deck.

---

## 🛠️ The Ship's Manifest (Tech Stack)

| Tech | Usage |
| :--- | :--- |
| **Vue.js 3** | The core framework driving the reactive UI and view-switching logic. |
| **Supabase** | Backend "Ledger" for real-time message logging and database management. |
| **REST API** | Used for seamless communication between the frontend and Supabase. |
| **CSS3 / Animations** | Custom keyframes for "Scam" shakes, floating elements, and smooth transitions. |
| **JavaScript (ES6+)** | Logic for the trap sequences, carousel timers, and state management. |

---

## 🏴‍☠️ Key Features

### 1. **The Marine Trap & Nullification**
A hidden logic gate where clicking "Report to Marines" triggers a red-alert loading screen. Users must "Eat the Devil Fruit" to nullify the effects and unlock the main navigation menu.

### 2. **Grand Line Training (Skills)**
A specialized section detailing technical proficiencies (Haki). It showcases the Captain’s growth in web development through a themed interface.

### 3. **The Captain’s Tale (Gallery)**
A sleek, auto-playing image carousel with a built-in lightbox feature. It chronicles the Captain's journey with smooth transitions and high-fidelity visuals.

### 4. **Battle Abilities & Pastimes**
Interactive sections that break down the Captain's "Combat Skills" (Technical Stack) and "Crew Pastimes" (Hobbies), providing a 360-degree view of the pirate's life.

### 5. **The Ship’s Ledger (Supabase Integration)**
A sleek, container-less messaging hub positioned to the left to preserve the background artwork.
* **Live Messaging:** Visitors can log their names and messages directly to the database.
* **Public Logs:** A real-time feed of the last 12 messages left by other visitors.
* **Invisible UI:** Features an invisible scrollbar for a clean look and high-resolution social icons (Den Den Mushi) for external contact.

---

## 🏗️ Technical Implementation Highlights

* **Dynamic Background Engine:** A custom system that swaps high-quality GIFs based on the `currentView`, ensuring the atmosphere matches the content.
* **Sleek UI/UX:** Content is strategically positioned to ensure major characters in the background art remain visible, utilizing `backdrop-filter` for readability.
* **Stealth Scrolling:** Implemented CSS `scrollbar-width: none` and `display: none` for webkit to maintain a minimalist aesthetic while allowing full message history browsing.

---

## 🚀 Installation & Launch

1.  **Clone the repository:**
    ```bash
    git clone [https://github.com/ushmaryosep/personal-website-finals-webprog.git](https://github.com/ushmaryosep/personal-website-finals-webprog.git)
    ```
2.  **Install dependencies:**
    ```bash
    npm install
    ```
3.  **Run the local server:**
    ```bash
    npm run serve
    ```
4.  **Build for production:**
    ```bash
    npm run build
    ```

---

> **"Wealth, fame, power... I left everything I gathered in one place. Now you just have to find it!"**
