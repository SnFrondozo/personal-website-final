<template>
  <div class="container">
    <!-- Navigation Bar -->
    <div class="nav-bar">
      <button v-for="section in sections" :key="section.id" @click="showSection(section.id)">
        {{ section.label }}
      </button>
    </div>

    <!-- Welcome Heading -->
    <h1>Welcome to My Portfolio</h1>

    <!-- Sections -->
    <section v-if="currentSection === 'about'">
      <h2>About Me</h2>
      <p>Hello! My name is <strong>Sondrick Frondozo</strong>. I'm a 3rd-year Bachelor of Science in Information Technology student.</p>
      <p>I am 23 years old, and I love **playing video games** and **reading novels & manhwa**!</p>
      <p>Nice to meet you! 🎮📖</p>
    </section>

    <section v-if="currentSection === 'education'">
      <h2>Education</h2>
      <p>📚 <strong>Bachelor of Science in Information Technology</strong></p>
    </section>

    <section v-if="currentSection === 'experience'">
      <h2>IT Experience</h2>
      <ul>
        <li>✅ Java</li>
        <li>✅ HTML, CSS, JavaScript</li>
        <li>✅ Mobile App Dev (Bamboo Warriors PH - Group Project)</li>
        <li>✅ MySQL</li>
      </ul>
    </section>

    <section v-if="currentSection === 'hobbies'">
      <h2>Hobbies & Interests</h2>
      <ul>
        <li>🎮 Gaming (Valorant, League of Legends, Dota 2, Gacha Games)</li>
        <li>🎶 Music (Ado, Yoasobi, Nightcore)</li>
        <li>📖 Novels (The Beginning After The End, Omniscient Reader’s Viewpoint)</li>
      </ul>
    </section>

    <section v-if="currentSection === 'goals'">
      <h2>Life Goals & Dreams</h2>
      <ul>
        <li>🎓 Graduate from College</li>
        <li>💻 Become a Successful Software Developer</li>
        <li>🌍 Travel the World</li>
        <li>👨‍🏫 Help Others Learn Coding</li>
        <li>🎹 Learn to Play Piano/Guitar</li>
      </ul>
    </section>

    <section v-if="currentSection === 'gallery'">
      <h2>🎮 Game Gallery</h2>
      <div class="gallery">
        <button @click="prevImage" class="nav-button">❮ Prev</button>
        <img :src="gameImages[currentImageIndex]" alt="Game Image" class="gallery-image"/>
        <button @click="nextImage" class="nav-button">Next ❯</button>
      </div>
    </section>
  </div>
</template>

<script>
import game1 from "@/gallery/game1.png";
import game2 from "@/gallery/game2.png";
import game3 from "@/gallery/game3.png";
import game4 from "@/gallery/game4.png";
import game5 from "@/gallery/game5.png";
import game6 from "@/gallery/game6.png";

export default {
  name: "Portfolio",
  data() {
    return {
      currentSection: "about",
      gameImages: [game1, game2, game3, game4, game5, game6],
      currentImageIndex: 0,
      sections: [
        { id: "about", label: "About" },
        { id: "education", label: "Education" },
        { id: "experience", label: "IT Experience" },
        { id: "hobbies", label: "Hobbies & Interests" },
        { id: "goals", label: "Goals" },
        { id: "gallery", label: "Game Gallery" }
      ]
    };
  },
  methods: {
    showSection(section) {
      this.currentSection = section;
    },
    nextImage() {
      this.currentImageIndex = (this.currentImageIndex + 1) % this.gameImages.length;
    },
    prevImage() {
      this.currentImageIndex = (this.currentImageIndex - 1 + this.gameImages.length) % this.gameImages.length;
    }
  },
};
</script>

<style>
/* General Styling */
body {
  background-color: #0a0a0a;
  color: #ff4444;
  font-family: "Poppins", sans-serif;
  text-align: center;
  margin: 0;
  padding: 0;
}

/* Container */
.container {
  max-width: 90%;
  margin: 30px auto;
  padding: 20px;
}

/* Navigation Bar */
.nav-bar {
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
  gap: 10px;
  margin-bottom: 20px;
}

.nav-bar button {
  background-color: #ff4444;
  border: none;
  padding: 15px 25px;
  font-size: 20px;
  color: white;
  cursor: pointer;
  border-radius: 5px;
  transition: 0.3s ease-in-out;
}

.nav-bar button:hover {
  background-color: #cc0000;
  transform: scale(1.1);
}

/* Sections */
section {
  background-color: rgba(50, 0, 0, 0.8);
  padding: 40px;
  border-radius: 10px;
  box-shadow: 0 0 15px rgba(255, 0, 0, 0.7);
  max-width: 900px;
  margin: 20px auto;
}

h1 {
  font-size: 2.8rem;
  font-weight: bold;
  text-shadow: 0 0 15px rgba(255, 0, 0, 0.7);
}

h2 {
  font-size: 2rem;
  color: #ffcccb;
  text-shadow: 0 0 10px rgba(255, 100, 100, 0.7);
}

/* Game Gallery */
.gallery {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 20px;
}

.gallery-image {
  width: 80%;
  max-width: 500px;
  height: auto;
  border-radius: 10px;
  box-shadow: 0px 4px 10px rgba(255, 0, 0, 0.6);
  transition: transform 0.3s ease-in-out;
}

.gallery-image:hover {
  transform: scale(1.05);
}

.nav-button {
  background-color: #ff4444;
  border: none;
  padding: 12px 18px;
  font-size: 20px;
  color: white;
  cursor: pointer;
  border-radius: 5px;
  transition: 0.3s ease-in-out;
}

.nav-button:hover {
  background-color: #cc0000;
  transform: scale(1.1);
}
</style>
