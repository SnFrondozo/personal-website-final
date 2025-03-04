<template>
  <div class="container">
    <!-- Navigation Bar-->
    <div class="nav-bar">
      <button @click="showSection('about')">About</button>
      <button @click="showSection('education')">Education</button>
      <button @click="showSection('experience')">IT Experience</button>
      <button @click="showSection('hobbies')">Hobbies & Interests</button>
      <button @click="showSection('goals')">Goals</button>
      <button @click="showSection('gallery')">Game Gallery</button>
    </div>

    <!-- Welcome Heading -->
    <h1>Welcome to My Portfolio</h1>

    <!-- Sections -->
    <section v-if="currentSection === 'about'">
      <h2>About Me</h2>
      <p>Hello! I'm a passionate developer with a love for technology and creativity.</p>
    </section>

    <section v-if="currentSection === 'education'">
      <h2>Education</h2>
      <p>Bachelor of Science in Information Technology</p>
      <p>Certified in [Relevant Certifications]</p>
    </section>

    <section v-if="currentSection === 'experience'">
      <h2>IT Experience</h2>
      <p>Worked on projects involving web and mobile development, including [specific technologies].</p>
    </section>

    <section v-if="currentSection === 'hobbies'">
      <h2>Hobbies & Interests</h2>
      <p>Gaming, coding, reading, traveling, and exploring new technologies.</p>
    </section>

    <section v-if="currentSection === 'goals'">
      <h2>6 Goals In Life / Dreams</h2>
      <p>Become a successful software developer</p>
      <p>Contribute to open-source projects</p>
      <p>Build my own tech startup</p>
      <p>Travel the world</p>
      <p>Help others learn coding</p>
      <p>Create a game or app that impacts millions</p>
    </section>

    <section v-if="currentSection === 'gallery'">
      <h2>Game Gallery</h2>
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

export default {
  name: "Portfolio",
  data() {
    return {
      currentSection: "about",
      gameImages: [game1, game2, game3],
      currentImageIndex: 0,
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
  background-color: #000;
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
  text-align: center;
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
  transition: 0.3s;
}

.nav-bar button:hover {
  background-color: #cc0000;
}

/* Welcome Title */
h1 {
  font-size: 2.5rem;
  margin-bottom: 20px;
}

/* Sections */
section {
  background-color: rgba(50, 0, 0, 0.8);
  padding: 40px;
  border-radius: 10px;
  box-shadow: 0 0 15px rgba(255, 0, 0, 0.7);
  width: 95%;
  max-width: 900px;
  margin: 20px auto;
}

h2 {
  font-size: 2rem;
}

p {
  font-size: 1.3rem;
  line-height: 1.6;
}

/* Game Gallery */
.gallery {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 20px;
  flex-wrap: wrap;
}

.gallery-image {
  width: 80%;
  max-width: 500px;
  height: auto;
  border-radius: 10px;
  box-shadow: 0px 4px 10px rgba(255, 0, 0, 0.6);
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}

.nav-button {
  background-color: #ff4444;
  border: none;
  padding: 12px 18px;
  font-size: 20px;
  color: white;
  cursor: pointer;
  border-radius: 5px;
  transition: 0.3s;
}

.nav-button:hover {
  background-color: #cc0000;
}

/* Mobile Responsiveness */
@media (max-width: 768px) {
  .container {
    width: 95%;
  }

  .nav-bar {
    flex-direction: column;
  }

  .nav-bar button {
    width: 100%;
    padding: 18px;
    font-size: 22px;
  }

  section {
    width: 100%;
    padding: 30px;
  }

  h1 {
    font-size: 2rem;
  }

  h2 {
    font-size: 1.8rem;
  }

  p {
    font-size: 1.2rem;
  }

  .gallery {
    flex-direction: column;
    align-items: center;
  }

  .gallery-image {
    width: 100%;
    max-width: 350px;
  }

  .nav-button {
    padding: 10px 15px;
    font-size: 18px;
  }
}
</style>