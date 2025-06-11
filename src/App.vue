<script setup>
import GlassNavbar from './components/GlassNavbar.vue'
import HeroSection from './components/HeroSection.vue'
import FormationsSection from './components/FormationsSection.vue'
import AboutSection from './components/AboutSection.vue'
import ContactSection from './components/ContactSection.vue'
</script>

<template>
  <div class="app-container">
    <GlassNavbar />

    <main>
      <HeroSection />
      <FormationsSection />
      <AboutSection />
      <ContactSection />
    </main>
  </div>
</template>

<style scoped>
.app-container {
  min-height: 100vh;
  background: linear-gradient(
    135deg,
    #667eea 0%,
    #764ba2 50%,
    #6B73FF 100%
  );
  position: relative;
}

.app-container::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background:
    radial-gradient(circle at 20% 80%, rgba(120, 119, 198, 0.3) 0%, transparent 50%),
    radial-gradient(circle at 80% 20%, rgba(255, 119, 198, 0.15) 0%, transparent 50%),
    radial-gradient(circle at 40% 40%, rgba(120, 219, 255, 0.15) 0%, transparent 50%);
  pointer-events: none;
}

main {
  position: relative;
  z-index: 1;
}

/* Optimisations responsives globales */
@media (max-width: 1024px) {
  .app-container::before {
    background:
      radial-gradient(circle at 25% 75%, rgba(120, 119, 198, 0.25) 0%, transparent 45%),
      radial-gradient(circle at 75% 25%, rgba(255, 119, 198, 0.12) 0%, transparent 45%),
      radial-gradient(circle at 45% 45%, rgba(120, 219, 255, 0.12) 0%, transparent 45%);
  }
}

@media (max-width: 768px) {
  .app-container {
    background: linear-gradient(
      135deg,
      #667eea 0%,
      #764ba2 40%,
      #6B73FF 100%
    );
  }

  .app-container::before {
    background:
      radial-gradient(circle at 30% 70%, rgba(120, 119, 198, 0.2) 0%, transparent 40%),
      radial-gradient(circle at 70% 30%, rgba(255, 119, 198, 0.1) 0%, transparent 40%);
  }
}

@media (max-width: 480px) {
  .app-container {
    background: linear-gradient(
      135deg,
      #667eea 0%,
      #764ba2 50%,
      #6B73FF 100%
    );
  }

  .app-container::before {
    background:
      radial-gradient(circle at 50% 50%, rgba(120, 119, 198, 0.15) 0%, transparent 35%);
  }
}

/* Gestion de l'orientation paysage */
@media (max-height: 600px) and (orientation: landscape) {
  .app-container::before {
    background:
      radial-gradient(circle at 30% 50%, rgba(120, 119, 198, 0.2) 0%, transparent 35%),
      radial-gradient(circle at 70% 50%, rgba(255, 119, 198, 0.1) 0%, transparent 35%);
  }
}

/* Optimisation pour les très petits écrans */
@media (max-width: 360px) {
  .app-container {
    min-height: 100vh;
    min-height: 100dvh; /* Nouvelle unité pour mobile */
  }
}

/* Support pour les écrans ultra-larges */
@media (min-width: 1920px) {
  .app-container::before {
    background:
      radial-gradient(circle at 15% 85%, rgba(120, 119, 198, 0.35) 0%, transparent 55%),
      radial-gradient(circle at 85% 15%, rgba(255, 119, 198, 0.18) 0%, transparent 55%),
      radial-gradient(circle at 35% 35%, rgba(120, 219, 255, 0.18) 0%, transparent 55%),
      radial-gradient(circle at 65% 65%, rgba(100, 200, 255, 0.1) 0%, transparent 40%);
  }
}
</style>
