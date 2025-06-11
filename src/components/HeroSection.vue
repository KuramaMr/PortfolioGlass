<template>
  <section id="home" class="hero-section">
    <div class="hero-container">
      <div class="hero-content">
        <div class="hero-card">
          <div class="profile-image">
            <div class="image-placeholder">
              <svg width="80" height="80" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
                <path d="M12 12c2.21 0 4-1.79 4-4s-1.79-4-4-4-4 1.79-4 4 1.79 4 4 4zm0 2c-2.67 0-8 1.34-8 4v2h16v-2c0-2.66-5.33-4-8-4z" fill="rgba(255,255,255,0.8)"/>
              </svg>
            </div>
          </div>

          <h1 class="hero-title">
            <span class="title-main">Jean Dupont</span>
            <span class="title-subtitle">Formateur CACES Indépendant</span>
          </h1>

          <p class="hero-description">
            Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
            Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.
          </p>

          <div class="hero-badges">
            <div class="badge">
              <span class="badge-number">15+</span>
              <span class="badge-text">Années d'expérience</span>
            </div>
            <div class="badge">
              <span class="badge-number">500+</span>
              <span class="badge-text">Stagiaires formés</span>
            </div>
            <div class="badge">
              <span class="badge-number">98%</span>
              <span class="badge-text">Taux de réussite</span>
            </div>
          </div>

          <div class="hero-actions">
            <button class="btn-primary" @click="scrollToSection('formations')">
              Découvrir mes formations
            </button>
            <button class="btn-secondary" @click="scrollToSection('contact')">
              Me contacter
            </button>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
const scrollToSection = (sectionId) => {
  const element = document.getElementById(sectionId);
  if (element) {
    element.scrollIntoView({ behavior: 'smooth' });
  }
}
</script>

<style scoped>
.hero-section {
  min-height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 120px 20px 60px;
  position: relative;
}

.hero-container {
  max-width: 800px;
  width: 100%;
}

.hero-content {
  text-align: center;
}

.hero-card {
  background: rgba(255, 255, 255, 0.1);
  backdrop-filter: blur(20px);
  -webkit-backdrop-filter: blur(20px);
  border: 1px solid rgba(255, 255, 255, 0.2);
  border-radius: 30px;
  padding: 60px 40px;
  box-shadow:
    0 20px 60px rgba(0, 0, 0, 0.1),
    inset 0 1px 0 rgba(255, 255, 255, 0.2);
  position: relative;
  overflow: hidden;
}

.hero-card::before {
  content: '';
  position: absolute;
  top: -50%;
  left: -50%;
  width: 200%;
  height: 200%;
  background: radial-gradient(
    circle at 30% 20%,
    rgba(255, 255, 255, 0.05) 0%,
    transparent 50%
  );
  pointer-events: none;
}

.profile-image {
  margin-bottom: 30px;
}

.image-placeholder {
  width: 120px;
  height: 120px;
  background: rgba(255, 255, 255, 0.15);
  border-radius: 50%;
  margin: 0 auto;
  display: flex;
  align-items: center;
  justify-content: center;
  border: 2px solid rgba(255, 255, 255, 0.3);
  box-shadow: 0 8px 32px rgba(0, 0, 0, 0.1);
}

.hero-title {
  margin-bottom: 30px;
}

.title-main {
  display: block;
  font-size: 3.5rem;
  font-weight: 700;
  color: rgba(255, 255, 255, 0.95);
  margin-bottom: 10px;
  text-shadow: 0 2px 10px rgba(0, 0, 0, 0.3);
}

.title-subtitle {
  display: block;
  font-size: 1.4rem;
  font-weight: 400;
  color: rgba(255, 255, 255, 0.8);
  text-shadow: 0 1px 5px rgba(0, 0, 0, 0.2);
}

.hero-description {
  font-size: 1.1rem;
  line-height: 1.7;
  color: rgba(255, 255, 255, 0.85);
  margin-bottom: 40px;
  max-width: 600px;
  margin-left: auto;
  margin-right: auto;
}

.hero-badges {
  display: flex;
  justify-content: center;
  gap: 30px;
  margin-bottom: 40px;
}

.badge {
  text-align: center;
  background: rgba(255, 255, 255, 0.1);
  backdrop-filter: blur(10px);
  border: 1px solid rgba(255, 255, 255, 0.2);
  border-radius: 20px;
  padding: 20px;
  min-width: 120px;
}

.badge-number {
  display: block;
  font-size: 2rem;
  font-weight: 700;
  color: rgba(255, 255, 255, 0.95);
  margin-bottom: 5px;
}

.badge-text {
  font-size: 0.9rem;
  color: rgba(255, 255, 255, 0.7);
  text-transform: uppercase;
  letter-spacing: 0.5px;
}

.hero-actions {
  display: flex;
  gap: 20px;
  justify-content: center;
  flex-wrap: wrap;
}

.btn-primary, .btn-secondary {
  padding: 15px 30px;
  border-radius: 50px;
  font-weight: 600;
  font-size: 1rem;
  border: none;
  cursor: pointer;
  transition: all 0.3s ease;
  backdrop-filter: blur(10px);
  -webkit-backdrop-filter: blur(10px);
  text-decoration: none;
  display: inline-block;
}

.btn-primary {
  background: rgba(255, 255, 255, 0.2);
  color: rgba(255, 255, 255, 0.95);
  border: 1px solid rgba(255, 255, 255, 0.3);
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);
}

.btn-primary:hover {
  background: rgba(255, 255, 255, 0.25);
  transform: translateY(-2px);
  box-shadow: 0 6px 20px rgba(0, 0, 0, 0.15);
}

.btn-secondary {
  background: transparent;
  color: rgba(255, 255, 255, 0.9);
  border: 2px solid rgba(255, 255, 255, 0.3);
}

.btn-secondary:hover {
  background: rgba(255, 255, 255, 0.1);
  border-color: rgba(255, 255, 255, 0.5);
  transform: translateY(-2px);
}

@media (max-width: 1024px) {
  .hero-section {
    padding: 100px 15px 50px;
  }

  .hero-card {
    padding: 50px 30px;
    margin: 0 15px;
  }

  .title-main {
    font-size: 3rem;
  }

  .hero-badges {
    flex-wrap: wrap;
    gap: 20px;
  }

  .badge {
    min-width: 100px;
  }
}

@media (max-width: 768px) {
  .hero-section {
    padding: 90px 10px 40px;
  }

  .hero-card {
    padding: 40px 20px;
    margin: 0 10px;
  }

  .title-main {
    font-size: 2.5rem;
  }

  .title-subtitle {
    font-size: 1.2rem;
  }

  .hero-description {
    font-size: 1rem;
    margin-bottom: 30px;
  }

  .hero-badges {
    flex-direction: column;
    gap: 15px;
    align-items: center;
    margin-bottom: 30px;
  }

  .badge {
    min-width: auto;
    width: 200px;
  }

  .hero-actions {
    flex-direction: column;
    align-items: center;
    gap: 15px;
  }

  .btn-primary, .btn-secondary {
    width: 250px;
    padding: 12px 25px;
  }
}

@media (max-width: 480px) {
  .hero-section {
    padding: 80px 5px 30px;
  }

  .hero-card {
    padding: 30px 15px;
    border-radius: 20px;
  }

  .image-placeholder {
    width: 100px;
    height: 100px;
  }

  .title-main {
    font-size: 2rem;
    margin-bottom: 8px;
  }

  .title-subtitle {
    font-size: 1.1rem;
  }

  .hero-description {
    font-size: 0.95rem;
    line-height: 1.6;
  }

  .badge {
    width: 180px;
    padding: 15px;
  }

  .badge-number {
    font-size: 1.8rem;
  }

  .badge-text {
    font-size: 0.8rem;
  }

  .btn-primary, .btn-secondary {
    width: 220px;
    font-size: 0.9rem;
  }
}

@media (max-width: 360px) {
  .hero-card {
    padding: 25px 10px;
  }

  .title-main {
    font-size: 1.8rem;
  }

  .hero-description {
    font-size: 0.9rem;
  }

  .btn-primary, .btn-secondary {
    width: 200px;
  }
}
</style>
