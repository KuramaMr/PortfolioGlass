<template>
  <section id="about" class="about-section">
    <div class="container">
      <div class="section-header">
        <h2 class="section-title">À Propos de Moi</h2>
        <p class="section-subtitle">
          Lorem ipsum dolor sit amet, consectetur adipiscing elit.
          Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
        </p>
      </div>

      <div class="about-content">
        <div class="about-card">
          <div class="about-text">
            <h3 class="about-title">Mon Parcours</h3>
            <p class="about-description">
              Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
              Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.
              Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
            </p>
            <p class="about-description">
              Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.
              Sed ut perspiciatis unde omnis iste natus error sit voluptatem accusantium doloremque laudantium.
            </p>
          </div>

          <div class="experience-timeline">
            <h3 class="timeline-title">Mon Expérience</h3>
            <div class="timeline">
              <div
                v-for="experience in experiences"
                :key="experience.id"
                class="timeline-item"
              >
                <div class="timeline-dot"></div>
                <div class="timeline-content">
                  <div class="timeline-year">{{ experience.year }}</div>
                  <h4 class="timeline-event-title">{{ experience.title }}</h4>
                  <p class="timeline-description">{{ experience.description }}</p>
                </div>
              </div>
            </div>
          </div>
        </div>

        <div class="skills-section">
          <h3 class="skills-title">Mes Compétences</h3>
          <div class="skills-grid">
            <div
              v-for="skill in skills"
              :key="skill.id"
              class="skill-card"
            >
              <div class="skill-icon">{{ skill.icon }}</div>
              <h4 class="skill-name">{{ skill.name }}</h4>
              <p class="skill-description">{{ skill.description }}</p>
            </div>
          </div>
        </div>

        <div class="values-section">
          <h3 class="values-title">Mes Valeurs</h3>
          <div class="values-grid">
            <div
              v-for="value in values"
              :key="value.id"
              class="value-card"
            >
              <div class="value-icon">{{ value.icon }}</div>
              <h4 class="value-name">{{ value.name }}</h4>
              <p class="value-description">{{ value.description }}</p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref } from 'vue'

const experiences = ref([
  {
    id: 1,
    year: '2023',
    title: 'Création de mon organisme de formation',
    description: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Lancement de mon activité de formation CACES indépendante.'
  },
  {
    id: 2,
    year: '2020',
    title: 'Certification Formateur CACES',
    description: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Obtention des certifications pour enseigner les formations CACES.'
  },
  {
    id: 3,
    year: '2015',
    title: 'Responsable Sécurité en Entreprise',
    description: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Gestion de la sécurité et formation des équipes.'
  },
  {
    id: 4,
    year: '2010',
    title: 'Début dans la conduite d\'engins',
    description: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Premiers pas dans le monde de la conduite d\'engins de chantier.'
  }
])

const skills = ref([
  {
    id: 1,
    name: 'Pédagogie',
    description: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit.',
    icon: '🎓'
  },
  {
    id: 2,
    name: 'Sécurité',
    description: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit.',
    icon: '🛡️'
  },
  {
    id: 3,
    name: 'Technique',
    description: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit.',
    icon: '⚙️'
  },
  {
    id: 4,
    name: 'Évaluation',
    description: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit.',
    icon: '📊'
  }
])

const values = ref([
  {
    id: 1,
    name: 'Excellence',
    description: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit.',
    icon: '⭐'
  },
  {
    id: 2,
    name: 'Bienveillance',
    description: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit.',
    icon: '💙'
  },
  {
    id: 3,
    name: 'Professionnalisme',
    description: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit.',
    icon: '🎯'
  }
])
</script>

<style scoped>
.about-section {
  padding: 80px 20px;
  position: relative;
}

.container {
  max-width: 1200px;
  margin: 0 auto;
}

.section-header {
  text-align: center;
  margin-bottom: 60px;
}

.section-title {
  font-size: 3rem;
  font-weight: 700;
  color: rgba(255, 255, 255, 0.95);
  margin-bottom: 20px;
  text-shadow: 0 2px 10px rgba(0, 0, 0, 0.3);
}

.section-subtitle {
  font-size: 1.2rem;
  color: rgba(255, 255, 255, 0.8);
  max-width: 600px;
  margin: 0 auto;
  line-height: 1.6;
}

.about-content {
  display: flex;
  flex-direction: column;
  gap: 60px;
}

.about-card {
  background: rgba(255, 255, 255, 0.1);
  backdrop-filter: blur(20px);
  -webkit-backdrop-filter: blur(20px);
  border: 1px solid rgba(255, 255, 255, 0.2);
  border-radius: 25px;
  padding: 50px;
  box-shadow:
    0 20px 60px rgba(0, 0, 0, 0.1),
    inset 0 1px 0 rgba(255, 255, 255, 0.2);
  position: relative;
  overflow: hidden;
}

.about-card::before {
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

.about-text {
  margin-bottom: 50px;
  position: relative;
  z-index: 1;
}

.about-title {
  font-size: 2rem;
  font-weight: 600;
  color: rgba(255, 255, 255, 0.95);
  margin-bottom: 25px;
}

.about-description {
  font-size: 1.1rem;
  line-height: 1.7;
  color: rgba(255, 255, 255, 0.85);
  margin-bottom: 20px;
}

.experience-timeline {
  position: relative;
  z-index: 1;
}

.timeline-title {
  font-size: 2rem;
  font-weight: 600;
  color: rgba(255, 255, 255, 0.95);
  margin-bottom: 30px;
}

.timeline {
  position: relative;
  padding-left: 30px;
}

.timeline::before {
  content: '';
  position: absolute;
  left: 15px;
  top: 0;
  bottom: 0;
  width: 2px;
  background: linear-gradient(to bottom,
    rgba(255, 255, 255, 0.3),
    rgba(255, 255, 255, 0.1)
  );
}

.timeline-item {
  position: relative;
  margin-bottom: 40px;
}

.timeline-dot {
  position: absolute;
  left: -22px;
  top: 8px;
  width: 12px;
  height: 12px;
  background: rgba(255, 255, 255, 0.8);
  border-radius: 50%;
  border: 3px solid rgba(255, 255, 255, 0.3);
  box-shadow: 0 0 0 4px rgba(255, 255, 255, 0.1);
}

.timeline-content {
  background: rgba(255, 255, 255, 0.05);
  border: 1px solid rgba(255, 255, 255, 0.1);
  border-radius: 15px;
  padding: 20px;
  margin-left: 20px;
}

.timeline-year {
  font-size: 0.9rem;
  font-weight: 600;
  color: rgba(255, 255, 255, 0.7);
  text-transform: uppercase;
  letter-spacing: 1px;
  margin-bottom: 8px;
}

.timeline-event-title {
  font-size: 1.2rem;
  font-weight: 600;
  color: rgba(255, 255, 255, 0.95);
  margin-bottom: 10px;
}

.timeline-description {
  color: rgba(255, 255, 255, 0.8);
  line-height: 1.5;
}

.skills-section, .values-section {
  text-align: center;
}

.skills-title, .values-title {
  font-size: 2.5rem;
  font-weight: 700;
  color: rgba(255, 255, 255, 0.95);
  margin-bottom: 40px;
  text-shadow: 0 2px 10px rgba(0, 0, 0, 0.3);
}

.skills-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 25px;
  margin-bottom: 40px;
}

.values-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
  gap: 25px;
}

.skill-card, .value-card {
  background: rgba(255, 255, 255, 0.08);
  backdrop-filter: blur(15px);
  border: 1px solid rgba(255, 255, 255, 0.15);
  border-radius: 20px;
  padding: 30px 25px;
  transition: all 0.3s ease;
}

.skill-card:hover, .value-card:hover {
  background: rgba(255, 255, 255, 0.12);
  transform: translateY(-5px);
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
}

.skill-icon, .value-icon {
  font-size: 2.5rem;
  margin-bottom: 15px;
}

.skill-name, .value-name {
  font-size: 1.3rem;
  font-weight: 600;
  color: rgba(255, 255, 255, 0.95);
  margin-bottom: 10px;
}

.skill-description, .value-description {
  color: rgba(255, 255, 255, 0.7);
  line-height: 1.5;
}

@media (max-width: 1024px) {
  .about-section {
    padding: 60px 15px;
  }

  .about-card {
    padding: 40px 30px;
  }

  .section-title {
    font-size: 2.8rem;
  }

  .skills-title, .values-title {
    font-size: 2.2rem;
  }

  .skills-grid {
    grid-template-columns: repeat(2, 1fr);
    gap: 20px;
  }

  .values-grid {
    grid-template-columns: repeat(2, 1fr);
    gap: 20px;
  }
}

@media (max-width: 768px) {
  .about-section {
    padding: 50px 10px;
  }

  .about-card {
    padding: 30px 20px;
  }

  .section-title {
    font-size: 2.5rem;
  }

  .about-title {
    font-size: 1.8rem;
  }

  .about-description {
    font-size: 1rem;
  }

  .timeline-title {
    font-size: 1.8rem;
  }

  .skills-title, .values-title {
    font-size: 2rem;
  }

  .skills-grid, .values-grid {
    grid-template-columns: 1fr;
  }

  .timeline {
    padding-left: 25px;
  }

  .timeline-content {
    margin-left: 15px;
  }

  .timeline-dot {
    left: -20px;
  }

  .timeline-event-title {
    font-size: 1.1rem;
  }

  .timeline-description {
    font-size: 0.95rem;
  }
}

@media (max-width: 480px) {
  .about-section {
    padding: 40px 8px;
  }

  .about-card {
    padding: 25px 15px;
    border-radius: 20px;
  }

  .section-title {
    font-size: 2.2rem;
  }

  .section-subtitle {
    font-size: 1rem;
    padding: 0 10px;
  }

  .about-title {
    font-size: 1.6rem;
    margin-bottom: 20px;
  }

  .about-description {
    font-size: 0.95rem;
    margin-bottom: 15px;
  }

  .timeline-title {
    font-size: 1.6rem;
    margin-bottom: 25px;
  }

  .timeline {
    padding-left: 20px;
  }

  .timeline-content {
    margin-left: 10px;
    padding: 15px;
  }

  .timeline-dot {
    left: -18px;
    width: 10px;
    height: 10px;
  }

  .timeline-year {
    font-size: 0.8rem;
  }

  .timeline-event-title {
    font-size: 1rem;
  }

  .timeline-description {
    font-size: 0.9rem;
  }

  .skills-title, .values-title {
    font-size: 1.8rem;
  }

  .skill-card, .value-card {
    padding: 25px 20px;
  }

  .skill-icon, .value-icon {
    font-size: 2.2rem;
  }

  .skill-name, .value-name {
    font-size: 1.2rem;
  }

  .skill-description, .value-description {
    font-size: 0.9rem;
  }
}

@media (max-width: 360px) {
  .about-section {
    padding: 30px 5px;
  }

  .about-card {
    padding: 20px 12px;
  }

  .section-title {
    font-size: 2rem;
  }

  .about-title {
    font-size: 1.5rem;
  }

  .timeline-title {
    font-size: 1.5rem;
  }

  .timeline-content {
    padding: 12px;
  }

  .timeline-event-title {
    font-size: 0.95rem;
  }

  .skills-title, .values-title {
    font-size: 1.6rem;
  }

  .skill-card, .value-card {
    padding: 20px 15px;
  }
}
</style>
