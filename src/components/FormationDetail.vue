<template>
  <div v-if="isVisible" class="formation-detail-overlay" @click="closeDetail">
    <div class="formation-detail-container" @click.stop>
      <button class="close-btn" @click="closeDetail">
        <svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
          <path d="M19 6.41L17.59 5 12 10.59 6.41 5 5 6.41 10.59 12 5 17.59 6.41 19 12 13.41 17.59 19 19 17.59 13.41 12z" fill="rgba(255,255,255,0.8)"/>
        </svg>
      </button>

      <div class="detail-content">
        <div class="detail-header">
          <div class="formation-icon">
            <component :is="formation?.icon" v-if="formation?.icon" />
          </div>
          <h1 class="formation-title">{{ formation?.title }}</h1>
          <p class="formation-subtitle">{{ formation?.description }}</p>
        </div>

        <div class="detail-body">
          <div class="detail-grid">
            <div class="detail-section">
              <h3 class="section-title">Informations Générales</h3>
              <div class="info-cards">
                <div class="info-card">
                  <div class="info-label">Durée de formation</div>
                  <div class="info-value">{{ formation?.duration }}</div>
                </div>
                <div class="info-card">
                  <div class="info-label">Validité</div>
                  <div class="info-value">{{ formation?.validity }}</div>
                </div>
                <div class="info-card">
                  <div class="info-label">Prix indicatif</div>
                  <div class="info-value">{{ formation?.price || 'Sur devis' }}</div>
                </div>
                <div class="info-card">
                  <div class="info-label">Participants max</div>
                  <div class="info-value">{{ formation?.maxParticipants || '8 personnes' }}</div>
                </div>
              </div>
            </div>

            <div class="detail-section">
              <h3 class="section-title">Catégories & Engins</h3>
              <div class="categories-grid">
                <div
                  v-for="category in formation?.categories"
                  :key="category.name"
                  class="category-card"
                >
                  <div class="category-name">{{ category.name }}</div>
                  <div class="category-description">{{ category.description }}</div>
                  <div class="category-engins">
                    <span
                      v-for="engin in category.engins"
                      :key="engin"
                      class="engin-badge"
                    >
                      {{ engin }}
                    </span>
                  </div>
                </div>
              </div>
            </div>

            <div class="detail-section">
              <h3 class="section-title">Programme de Formation</h3>
              <div class="program-timeline">
                <div
                  v-for="(module, index) in formation?.program"
                  :key="index"
                  class="program-module"
                >
                  <div class="module-number">{{ index + 1 }}</div>
                  <div class="module-content">
                    <h4 class="module-title">{{ module.title }}</h4>
                    <p class="module-description">{{ module.description }}</p>
                    <div class="module-duration">{{ module.duration }}</div>
                  </div>
                </div>
              </div>
            </div>

            <div class="detail-section">
              <h3 class="section-title">Prérequis & Conditions</h3>
              <div class="requirements-grid">
                <div class="requirement-card">
                  <h4 class="req-title">🎯 Prérequis</h4>
                  <ul class="req-list">
                    <li v-for="req in formation?.prerequisites" :key="req">{{ req }}</li>
                  </ul>
                </div>
                <div class="requirement-card">
                  <h4 class="req-title">📋 Documents nécessaires</h4>
                  <ul class="req-list">
                    <li v-for="doc in formation?.requiredDocuments" :key="doc">{{ doc }}</li>
                  </ul>
                </div>
                <div class="requirement-card">
                  <h4 class="req-title">🏥 Aptitudes médicales</h4>
                  <ul class="req-list">
                    <li v-for="medical in formation?.medicalRequirements" :key="medical">{{ medical }}</li>
                  </ul>
                </div>
              </div>
            </div>

            <div class="detail-section">
              <h3 class="section-title">Évaluation & Certification</h3>
              <div class="evaluation-content">
                <div class="eval-card">
                  <h4 class="eval-title">📝 Épreuve Théorique</h4>
                  <p class="eval-description">{{ formation?.theoreticalTest }}</p>
                </div>
                <div class="eval-card">
                  <h4 class="eval-title">🚛 Épreuve Pratique</h4>
                  <p class="eval-description">{{ formation?.practicalTest }}</p>
                </div>
                <div class="eval-card">
                  <h4 class="eval-title">🏆 Certification</h4>
                  <p class="eval-description">{{ formation?.certification }}</p>
                </div>
              </div>
            </div>
          </div>
        </div>

        <div class="detail-footer">
          <div class="contact-cta">
            <h3 class="cta-title">Intéressé par cette formation ?</h3>
            <p class="cta-description">Contactez-moi pour un devis personnalisé ou pour planifier votre formation.</p>
            <div class="cta-buttons">
              <button class="btn-primary" @click="scrollToContact">
                Demander un devis
              </button>
              <button class="btn-secondary" @click="closeDetail">
                Voir toutes les formations
              </button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { watch } from 'vue'

const props = defineProps({
  formation: {
    type: Object,
    default: null
  },
  isVisible: {
    type: Boolean,
    default: false
  }
})

const emit = defineEmits(['close'])

const closeDetail = () => {
  emit('close')
}

const scrollToContact = () => {
  closeDetail()
  setTimeout(() => {
    const contactSection = document.getElementById('contact')
    if (contactSection) {
      contactSection.scrollIntoView({ behavior: 'smooth' })
    }
  }, 300)
}

// Empêcher le scroll du body quand la modal est ouverte
watch(() => props.isVisible, (newValue) => {
  if (newValue) {
    document.body.style.overflow = 'hidden'
  } else {
    document.body.style.overflow = ''
  }
})
</script>

<style scoped>
.formation-detail-overlay {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: rgba(0, 0, 0, 0.7);
  backdrop-filter: blur(10px);
  z-index: 9999;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 20px;
  overflow-y: auto;
  overflow-x: hidden;
  box-sizing: border-box;
}

.formation-detail-container {
  background: rgba(255, 255, 255, 0.1);
  backdrop-filter: blur(25px);
  -webkit-backdrop-filter: blur(25px);
  border: 1px solid rgba(255, 255, 255, 0.2);
  border-radius: 25px;
  max-width: 1000px;
  width: 100%;
  max-height: 90vh;
  overflow-y: auto;
  overflow-x: hidden;
  position: relative;
  box-shadow: 0 30px 80px rgba(0, 0, 0, 0.3);
  margin-top: 80px;
  margin-bottom: 20px;
  box-sizing: border-box;
}

.formation-detail-container::before {
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

.close-btn {
  position: absolute;
  top: 20px;
  right: 20px;
  background: rgba(255, 255, 255, 0.1);
  border: 1px solid rgba(255, 255, 255, 0.2);
  border-radius: 50%;
  width: 40px;
  height: 40px;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  transition: all 0.3s ease;
  z-index: 10;
}

.close-btn:hover {
  background: rgba(255, 255, 255, 0.2);
  transform: scale(1.1);
}

.detail-content {
  padding: 40px;
  position: relative;
  z-index: 1;
  width: 100%;
  box-sizing: border-box;
  overflow-x: hidden;
}

.detail-header {
  text-align: center;
  margin-bottom: 40px;
}

.formation-icon {
  margin-bottom: 20px;
}

.formation-title {
  font-size: 2.5rem;
  font-weight: 700;
  color: rgba(255, 255, 255, 0.95);
  margin-bottom: 15px;
  text-shadow: 0 2px 10px rgba(0, 0, 0, 0.3);
}

.formation-subtitle {
  font-size: 1.2rem;
  color: rgba(255, 255, 255, 0.8);
  line-height: 1.6;
  max-width: 600px;
  margin: 0 auto;
}

.detail-body {
  margin-bottom: 40px;
}

.detail-section {
  margin-bottom: 50px;
}

.section-title {
  font-size: 1.8rem;
  font-weight: 600;
  color: rgba(255, 255, 255, 0.95);
  margin-bottom: 25px;
  text-align: center;
}

.info-cards {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  gap: 20px;
  margin-bottom: 30px;
  width: 100%;
  box-sizing: border-box;
}

.info-card {
  background: rgba(255, 255, 255, 0.08);
  border: 1px solid rgba(255, 255, 255, 0.15);
  border-radius: 15px;
  padding: 20px;
  text-align: center;
}

.info-label {
  font-size: 0.9rem;
  color: rgba(255, 255, 255, 0.7);
  text-transform: uppercase;
  letter-spacing: 0.5px;
  margin-bottom: 8px;
}

.info-value {
  font-size: 1.1rem;
  font-weight: 600;
  color: rgba(255, 255, 255, 0.95);
}

.categories-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
  gap: 20px;
  width: 100%;
  box-sizing: border-box;
}

.category-card {
  background: rgba(255, 255, 255, 0.08);
  border: 1px solid rgba(255, 255, 255, 0.15);
  border-radius: 15px;
  padding: 25px;
  box-sizing: border-box;
  width: 100%;
  max-width: 100%;
}

.category-name {
  font-size: 1.2rem;
  font-weight: 600;
  color: rgba(255, 255, 255, 0.95);
  margin-bottom: 10px;
}

.category-description {
  color: rgba(255, 255, 255, 0.8);
  margin-bottom: 15px;
  line-height: 1.5;
}

.category-engins {
  display: flex;
  flex-wrap: wrap;
  gap: 8px;
}

.engin-badge {
  background: rgba(255, 255, 255, 0.15);
  color: rgba(255, 255, 255, 0.9);
  padding: 4px 10px;
  border-radius: 10px;
  font-size: 0.8rem;
  font-weight: 500;
}

.program-timeline {
  display: flex;
  flex-direction: column;
  gap: 25px;
}

.program-module {
  display: flex;
  align-items: flex-start;
  gap: 20px;
  background: rgba(255, 255, 255, 0.05);
  border: 1px solid rgba(255, 255, 255, 0.1);
  border-radius: 15px;
  padding: 25px;
}

.module-number {
  background: rgba(255, 255, 255, 0.2);
  color: rgba(255, 255, 255, 0.95);
  width: 40px;
  height: 40px;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  font-weight: 600;
  font-size: 1.1rem;
  flex-shrink: 0;
}

.module-content {
  flex: 1;
}

.module-title {
  font-size: 1.2rem;
  font-weight: 600;
  color: rgba(255, 255, 255, 0.95);
  margin-bottom: 10px;
}

.module-description {
  color: rgba(255, 255, 255, 0.8);
  line-height: 1.6;
  margin-bottom: 10px;
}

.module-duration {
  color: rgba(255, 255, 255, 0.7);
  font-size: 0.9rem;
  font-weight: 500;
}

.requirements-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 25px;
}

.requirement-card {
  background: rgba(255, 255, 255, 0.08);
  border: 1px solid rgba(255, 255, 255, 0.15);
  border-radius: 15px;
  padding: 25px;
}

.req-title {
  font-size: 1.1rem;
  font-weight: 600;
  color: rgba(255, 255, 255, 0.95);
  margin-bottom: 15px;
}

.req-list {
  list-style: none;
  padding: 0;
  margin: 0;
}

.req-list li {
  color: rgba(255, 255, 255, 0.8);
  padding: 5px 0;
  padding-left: 20px;
  position: relative;
}

.req-list li::before {
  content: '•';
  color: rgba(255, 255, 255, 0.6);
  position: absolute;
  left: 0;
}

.evaluation-content {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
  gap: 20px;
}

.eval-card {
  background: rgba(255, 255, 255, 0.08);
  border: 1px solid rgba(255, 255, 255, 0.15);
  border-radius: 15px;
  padding: 25px;
}

.eval-title {
  font-size: 1.1rem;
  font-weight: 600;
  color: rgba(255, 255, 255, 0.95);
  margin-bottom: 15px;
}

.eval-description {
  color: rgba(255, 255, 255, 0.8);
  line-height: 1.6;
}

.detail-footer {
  border-top: 1px solid rgba(255, 255, 255, 0.1);
  padding-top: 30px;
}

.contact-cta {
  text-align: center;
}

.cta-title {
  font-size: 1.8rem;
  font-weight: 600;
  color: rgba(255, 255, 255, 0.95);
  margin-bottom: 15px;
}

.cta-description {
  color: rgba(255, 255, 255, 0.8);
  margin-bottom: 25px;
  line-height: 1.6;
}

.cta-buttons {
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
}

.btn-primary {
  background: rgba(255, 255, 255, 0.2);
  color: rgba(255, 255, 255, 0.95);
  border: 1px solid rgba(255, 255, 255, 0.3);
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
  .formation-detail-overlay {
    padding: 15px;
  }

  .formation-detail-container {
    max-width: 900px;
  }

  .detail-content {
    padding: 35px 30px;
  }

  .formation-title {
    font-size: 2.3rem;
  }

  .info-cards {
    grid-template-columns: repeat(2, 1fr);
    gap: 15px;
  }

  .categories-grid, .requirements-grid, .evaluation-content {
    grid-template-columns: repeat(2, 1fr);
    gap: 15px;
  }
}

@media (max-width: 768px) {
  .formation-detail-overlay {
    padding: 10px;
  }

  .detail-content {
    padding: 30px 20px;
  }

  .formation-title {
    font-size: 2rem;
  }

  .formation-subtitle {
    font-size: 1.1rem;
  }

  .section-title {
    font-size: 1.6rem;
  }

  .info-cards {
    grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
  }

  .categories-grid, .requirements-grid, .evaluation-content {
    grid-template-columns: 1fr;
  }

  .program-module {
    flex-direction: column;
    text-align: center;
    gap: 15px;
  }

  .module-number {
    margin: 0 auto;
  }

  .cta-buttons {
    flex-direction: column;
    align-items: center;
  }

  .btn-primary, .btn-secondary {
    width: 250px;
  }

  .cta-title {
    font-size: 1.6rem;
  }
}

@media (max-width: 480px) {
  .formation-detail-overlay {
    padding: 8px;
    align-items: flex-start;
    padding-top: 70px;
    overflow-x: hidden;
  }

  .formation-detail-container {
    max-height: calc(100vh - 80px);
    border-radius: 20px;
    margin-top: 0;
    margin-bottom: 10px;
    width: calc(100% - 16px);
    max-width: calc(100% - 16px);
  }

  .close-btn {
    top: 15px;
    right: 15px;
    width: 35px;
    height: 35px;
    background: rgba(255, 255, 255, 0.2);
    border: 2px solid rgba(255, 255, 255, 0.3);
  }

  .detail-content {
    padding: 25px 15px;
    width: calc(100% - 30px);
  }

  .formation-title {
    font-size: 1.8rem;
    margin-bottom: 12px;
    word-wrap: break-word;
    hyphens: auto;
  }

  .formation-subtitle {
    font-size: 1rem;
    word-wrap: break-word;
  }

  .detail-section {
    margin-bottom: 35px;
    width: 100%;
  }

  .section-title {
    font-size: 1.5rem;
    margin-bottom: 20px;
    word-wrap: break-word;
  }

  .info-cards {
    grid-template-columns: repeat(2, 1fr);
    gap: 12px;
    width: 100%;
  }

  .info-card {
    padding: 15px;
    min-width: 0;
    word-wrap: break-word;
  }

  .info-label {
    font-size: 0.8rem;
  }

  .info-value {
    font-size: 1rem;
    word-wrap: break-word;
  }

  .category-card, .requirement-card, .eval-card {
    padding: 20px;
    min-width: 0;
    word-wrap: break-word;
  }

  .category-name, .req-title, .eval-title {
    font-size: 1rem;
    word-wrap: break-word;
  }

  .category-description, .eval-description {
    font-size: 0.9rem;
    word-wrap: break-word;
  }

  .req-list li {
    font-size: 0.9rem;
    word-wrap: break-word;
  }

  .program-module {
    padding: 20px;
    min-width: 0;
    word-wrap: break-word;
  }

  .module-number {
    width: 35px;
    height: 35px;
    font-size: 1rem;
  }

  .module-title {
    font-size: 1.1rem;
    word-wrap: break-word;
  }

  .module-description {
    font-size: 0.9rem;
    word-wrap: break-word;
  }

  .module-duration {
    font-size: 0.85rem;
  }

  .cta-title {
    font-size: 1.5rem;
    word-wrap: break-word;
  }

  .cta-description {
    font-size: 0.95rem;
    word-wrap: break-word;
  }

  .btn-primary, .btn-secondary {
    width: 220px;
    max-width: 100%;
    padding: 12px 25px;
    font-size: 0.9rem;
    word-wrap: break-word;
  }
}

@media (max-width: 360px) {
  .formation-detail-overlay {
    padding: 5px;
    padding-top: 60px;
    overflow-x: hidden;
  }

  .formation-detail-container {
    max-height: calc(100vh - 70px);
    width: calc(100% - 10px);
    max-width: calc(100% - 10px);
  }

  .close-btn {
    top: 10px;
    right: 10px;
    width: 32px;
    height: 32px;
  }

  .detail-content {
    padding: 20px 12px;
    width: calc(100% - 24px);
  }

  .formation-title {
    font-size: 1.6rem;
    word-wrap: break-word;
    hyphens: auto;
  }

  .formation-subtitle {
    font-size: 0.95rem;
    word-wrap: break-word;
  }

  .section-title {
    font-size: 1.4rem;
    word-wrap: break-word;
  }

  .info-cards {
    grid-template-columns: 1fr;
    gap: 10px;
    width: 100%;
  }

  .info-card {
    padding: 12px;
    min-width: 0;
    word-wrap: break-word;
  }

  .category-card, .requirement-card, .eval-card {
    padding: 15px;
    min-width: 0;
    word-wrap: break-word;
  }

  .program-module {
    padding: 15px;
    min-width: 0;
    word-wrap: break-word;
  }

  .module-number {
    width: 30px;
    height: 30px;
    font-size: 0.9rem;
  }

  .module-title {
    font-size: 1rem;
    word-wrap: break-word;
  }

  .btn-primary, .btn-secondary {
    width: 200px;
    max-width: 100%;
    padding: 10px 20px;
    font-size: 0.85rem;
    word-wrap: break-word;
  }
}

/* Améliorations pour les très petits écrans et l'orientation paysage */
@media (max-height: 600px) and (orientation: landscape) {
  .formation-detail-overlay {
    align-items: flex-start;
    padding-top: 10px;
  }

  .formation-detail-container {
    max-height: 95vh;
  }

  .detail-content {
    padding: 20px 15px;
  }

  .detail-section {
    margin-bottom: 25px;
  }
}
</style>
