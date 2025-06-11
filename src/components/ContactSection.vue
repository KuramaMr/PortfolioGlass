<template>
  <section id="contact" class="contact-section">
    <div class="container">
      <div class="section-header">
        <h2 class="section-title">Me Contacter</h2>
        <p class="section-subtitle">
          Lorem ipsum dolor sit amet, consectetur adipiscing elit.
          N'hésitez pas à me contacter pour toute question sur mes formations.
        </p>
      </div>

      <div class="contact-content">
        <div class="contact-info">
          <div class="info-card">
            <h3 class="card-title">Informations de Contact</h3>

            <div class="contact-item">
              <div class="contact-icon">
                <svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
                  <path d="M6.62 10.79c1.44 2.83 3.76 5.14 6.59 6.59l2.2-2.2c.27-.27.67-.36 1.02-.24 1.12.37 2.33.57 3.57.57.55 0 1 .45 1 1V20c0 .55-.45 1-1 1-9.39 0-17-7.61-17-17 0-.55.45-1 1-1h3.5c.55 0 1 .45 1 1 0 1.25.2 2.45.57 3.57.11.35.03.74-.25 1.02l-2.2 2.2z" fill="rgba(255,255,255,0.8)"/>
                </svg>
              </div>
              <div class="contact-details">
                <span class="contact-label">Téléphone</span>
                <span class="contact-value">06 12 34 56 78</span>
              </div>
            </div>

            <div class="contact-item">
              <div class="contact-icon">
                <svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
                  <path d="M20 4H4c-1.1 0-1.99.9-1.99 2L2 18c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 4l-8 5-8-5V6l8 5 8-5v2z" fill="rgba(255,255,255,0.8)"/>
                </svg>
              </div>
              <div class="contact-details">
                <span class="contact-label">Email</span>
                <span class="contact-value">jean.dupont@formation-caces.fr</span>
              </div>
            </div>

            <div class="contact-item">
              <div class="contact-icon">
                <svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
                  <path d="M12 2C8.13 2 5 5.13 5 9c0 5.25 7 13 7 13s7-7.75 7-13c0-3.87-3.13-7-7-7zm0 9.5c-1.38 0-2.5-1.12-2.5-2.5s1.12-2.5 2.5-2.5 2.5 1.12 2.5 2.5-1.12 2.5-2.5 2.5z" fill="rgba(255,255,255,0.8)"/>
                </svg>
              </div>
              <div class="contact-details">
                <span class="contact-label">Zone d'intervention</span>
                <span class="contact-value">Région Île-de-France et départements limitrophes</span>
              </div>
            </div>

            <div class="contact-item">
              <div class="contact-icon">
                <svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
                  <path d="M11.99 2C6.47 2 2 6.48 2 12s4.47 10 9.99 10C17.52 22 22 17.52 22 12S17.52 2 11.99 2zM12 20c-4.42 0-8-3.58-8-8s3.58-8 8-8 8 3.58 8 8-3.58 8-8 8z" fill="rgba(255,255,255,0.8)"/>
                  <path d="M12.5 7H11v6l5.25 3.15.75-1.23-4.5-2.67z" fill="rgba(255,255,255,0.8)"/>
                </svg>
              </div>
              <div class="contact-details">
                <span class="contact-label">Horaires</span>
                <div class="contact-value">
                  <div class="horaire-line">Lun-Ven : 8h-18h</div>
                  <div class="horaire-line">Sam : 8h-12h</div>
                </div>
              </div>
            </div>
          </div>
        </div>

        <div class="contact-form-section">
          <div class="form-card">
            <h3 class="card-title">Demande de Renseignements</h3>
            <form @submit.prevent="handleSubmit" class="contact-form">
              <div class="form-group">
                <label for="name" class="form-label">Nom complet *</label>
                <input
                  type="text"
                  id="name"
                  v-model="form.name"
                  class="form-input"
                  placeholder="Votre nom complet"
                  required
                >
              </div>

              <div class="form-group">
                <label for="email" class="form-label">Email *</label>
                <input
                  type="email"
                  id="email"
                  v-model="form.email"
                  class="form-input"
                  placeholder="votre.email@example.com"
                  required
                >
              </div>

              <div class="form-group">
                <label for="phone" class="form-label">Téléphone</label>
                <input
                  type="tel"
                  id="phone"
                  v-model="form.phone"
                  class="form-input"
                  placeholder="06 12 34 56 78"
                >
              </div>

              <div class="form-group">
                <label for="formation" class="form-label">Formation souhaitée</label>
                <select
                  id="formation"
                  v-model="form.formation"
                  class="form-select"
                >
                  <option value="">Sélectionnez une formation</option>
                  <option value="caces-r489">CACES R489 - Chariots élévateurs</option>
                  <option value="caces-r482">CACES R482 - Engins de chantier</option>
                  <option value="caces-r487">CACES R487 - Grues mobiles</option>
                  <option value="caces-r486">CACES R486 - PEMP</option>
                  <option value="autre">Autre formation</option>
                </select>
              </div>

              <div class="form-group">
                <label for="message" class="form-label">Message *</label>
                <textarea
                  id="message"
                  v-model="form.message"
                  class="form-textarea"
                  rows="5"
                  placeholder="Décrivez votre demande, vos besoins en formation, nombre de personnes à former, dates souhaitées..."
                  required
                ></textarea>
              </div>

              <button type="submit" class="submit-btn" :disabled="isSubmitting">
                <span v-if="!isSubmitting">Envoyer ma demande</span>
                <span v-else>Envoi en cours...</span>
              </button>
            </form>
          </div>
        </div>
      </div>

      <div class="additional-info">
        <div class="info-grid">
          <div class="info-item">
            <div class="info-icon">📋</div>
            <h4 class="info-title">Devis Gratuit</h4>
            <p class="info-description">Lorem ipsum dolor sit amet, consectetur adipiscing elit.</p>
          </div>
          <div class="info-item">
            <div class="info-icon">🚀</div>
            <h4 class="info-title">Réponse Rapide</h4>
            <p class="info-description">Lorem ipsum dolor sit amet, consectetur adipiscing elit.</p>
          </div>
          <div class="info-item">
            <div class="info-icon">📍</div>
            <h4 class="info-title">Déplacement</h4>
            <p class="info-description">Lorem ipsum dolor sit amet, consectetur adipiscing elit.</p>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, reactive } from 'vue'

const isSubmitting = ref(false)

const form = reactive({
  name: '',
  email: '',
  phone: '',
  formation: '',
  message: ''
})

const handleSubmit = async () => {
  isSubmitting.value = true

  // Simulation d'envoi
  setTimeout(() => {
    alert('Merci pour votre message ! Je vous répondrai dans les plus brefs délais.')

    // Reset du formulaire
    Object.keys(form).forEach(key => {
      form[key] = ''
    })

    isSubmitting.value = false
  }, 1000)
}
</script>

<style scoped>
.contact-section {
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

.contact-content {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 40px;
  margin-bottom: 60px;
}

.info-card, .form-card {
  background: rgba(255, 255, 255, 0.1);
  backdrop-filter: blur(20px);
  -webkit-backdrop-filter: blur(20px);
  border: 1px solid rgba(255, 255, 255, 0.2);
  border-radius: 25px;
  padding: 40px;
  box-shadow:
    0 20px 60px rgba(0, 0, 0, 0.1),
    inset 0 1px 0 rgba(255, 255, 255, 0.2);
  position: relative;
  overflow: hidden;
}

.info-card::before, .form-card::before {
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

.card-title {
  font-size: 1.8rem;
  font-weight: 600;
  color: rgba(255, 255, 255, 0.95);
  margin-bottom: 30px;
  position: relative;
  z-index: 1;
}

.contact-item {
  display: flex;
  align-items: flex-start;
  margin-bottom: 25px;
  position: relative;
  z-index: 1;
}

.contact-icon {
  background: rgba(255, 255, 255, 0.1);
  border-radius: 12px;
  padding: 12px;
  margin-right: 15px;
  border: 1px solid rgba(255, 255, 255, 0.2);
}

.contact-details {
  flex: 1;
}

.contact-label {
  display: block;
  font-size: 0.9rem;
  font-weight: 600;
  color: rgba(255, 255, 255, 0.7);
  text-transform: uppercase;
  letter-spacing: 0.5px;
  margin-bottom: 5px;
}

.contact-value {
  color: rgba(255, 255, 255, 0.9);
  font-size: 1rem;
  line-height: 1.4;
}

.horaire-line {
  margin-bottom: 3px;
}

.horaire-line:last-child {
  margin-bottom: 0;
}

.contact-form {
  position: relative;
  z-index: 1;
}

.form-group {
  margin-bottom: 25px;
}

.form-label {
  display: block;
  font-size: 0.9rem;
  font-weight: 600;
  color: rgba(255, 255, 255, 0.8);
  margin-bottom: 8px;
}

.form-input, .form-select, .form-textarea {
  width: 100%;
  background: rgba(255, 255, 255, 0.1);
  border: 1px solid rgba(255, 255, 255, 0.2);
  border-radius: 12px;
  padding: 12px 16px;
  color: rgba(255, 255, 255, 0.9);
  font-size: 1rem;
  transition: all 0.3s ease;
  backdrop-filter: blur(10px);
}

.form-input::placeholder, .form-textarea::placeholder {
  color: rgba(255, 255, 255, 0.5);
}

.form-input:focus, .form-select:focus, .form-textarea:focus {
  outline: none;
  border-color: rgba(255, 255, 255, 0.4);
  background: rgba(255, 255, 255, 0.15);
  box-shadow: 0 0 0 3px rgba(255, 255, 255, 0.1);
}

.form-textarea {
  resize: vertical;
  min-height: 120px;
}

.form-select {
  background: rgba(255, 255, 255, 0.15);
  cursor: pointer;
}

.form-select option {
  background: rgba(50, 50, 80, 0.95);
  color: rgba(255, 255, 255, 0.9);
  padding: 10px;
  border: none;
}

.form-select option:hover {
  background: rgba(70, 70, 100, 0.95);
}

.form-select option:checked {
  background: rgba(90, 90, 120, 0.95);
}

.submit-btn {
  width: 100%;
  background: rgba(255, 255, 255, 0.2);
  color: rgba(255, 255, 255, 0.95);
  border: 1px solid rgba(255, 255, 255, 0.3);
  border-radius: 50px;
  padding: 15px 30px;
  font-size: 1rem;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.3s ease;
  backdrop-filter: blur(10px);
}

.submit-btn:hover:not(:disabled) {
  background: rgba(255, 255, 255, 0.25);
  transform: translateY(-2px);
  box-shadow: 0 6px 20px rgba(0, 0, 0, 0.15);
}

.submit-btn:disabled {
  opacity: 0.6;
  cursor: not-allowed;
}

.additional-info {
  text-align: center;
}

.info-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 25px;
}

.info-item {
  background: rgba(255, 255, 255, 0.08);
  backdrop-filter: blur(15px);
  border: 1px solid rgba(255, 255, 255, 0.15);
  border-radius: 20px;
  padding: 30px 25px;
  transition: all 0.3s ease;
}

.info-item:hover {
  background: rgba(255, 255, 255, 0.12);
  transform: translateY(-5px);
}

.info-icon {
  font-size: 2.5rem;
  margin-bottom: 15px;
}

.info-title {
  font-size: 1.3rem;
  font-weight: 600;
  color: rgba(255, 255, 255, 0.95);
  margin-bottom: 10px;
}

.info-description {
  color: rgba(255, 255, 255, 0.7);
  line-height: 1.5;
}

@media (max-width: 1024px) {
  .contact-section {
    padding: 60px 15px;
  }

  .section-title {
    font-size: 2.8rem;
  }

  .contact-content {
    gap: 30px;
  }

  .info-card, .form-card {
    padding: 35px 25px;
  }
}

@media (max-width: 768px) {
  .contact-section {
    padding: 50px 10px;
  }

  .section-title {
    font-size: 2.5rem;
  }

  .section-subtitle {
    font-size: 1.1rem;
  }

  .contact-content {
    grid-template-columns: 1fr;
    gap: 30px;
  }

  .info-card, .form-card {
    padding: 30px 20px;
  }

  .card-title {
    font-size: 1.6rem;
  }

  .contact-item {
    margin-bottom: 18px;
    flex-direction: column;
    text-align: center;
    gap: 10px;
    align-items: center;
  }

  .contact-icon {
    margin: 0 auto;
    margin-bottom: 8px;
  }

  .contact-details {
    text-align: center;
  }

  .contact-label {
    font-size: 0.85rem;
  }

  .contact-value {
    font-size: 0.95rem;
  }

  .form-group {
    margin-bottom: 20px;
  }

  .form-label {
    font-size: 0.85rem;
  }

  .form-input, .form-select, .form-textarea {
    padding: 10px 14px;
    font-size: 0.95rem;
  }

  .submit-btn {
    padding: 12px 25px;
    font-size: 0.95rem;
  }

  .info-grid {
    grid-template-columns: 1fr;
  }

  .info-item {
    padding: 25px 20px;
  }

  .info-title {
    font-size: 1.2rem;
  }

  .info-description {
    font-size: 0.9rem;
  }
}

@media (max-width: 480px) {
  .contact-section {
    padding: 40px 8px;
  }

  .section-title {
    font-size: 2.2rem;
  }

  .section-subtitle {
    font-size: 1rem;
    padding: 0 10px;
  }

  .info-card, .form-card {
    padding: 25px 15px;
    border-radius: 20px;
  }

  .card-title {
    font-size: 1.5rem;
    margin-bottom: 25px;
  }

  .contact-item {
    margin-bottom: 18px;
    flex-direction: column;
    text-align: center;
    gap: 10px;
    align-items: center;
  }

  .contact-icon {
    margin: 0 auto;
    margin-bottom: 8px;
  }

  .contact-details {
    text-align: center;
  }

  .contact-label {
    font-size: 0.8rem;
  }

  .contact-value {
    font-size: 0.9rem;
  }

  .form-group {
    margin-bottom: 18px;
  }

  .form-input, .form-select, .form-textarea {
    padding: 10px 12px;
    font-size: 0.9rem;
    border-radius: 10px;
  }

  .form-textarea {
    min-height: 100px;
  }

  .submit-btn {
    padding: 12px 20px;
    font-size: 0.9rem;
  }

  .cta-title {
    font-size: 1.6rem;
  }

  .cta-description {
    font-size: 0.95rem;
    margin-bottom: 20px;
  }

  .info-item {
    padding: 20px 15px;
  }

  .info-icon {
    font-size: 2.2rem;
  }

  .info-title {
    font-size: 1.1rem;
  }

  .info-description {
    font-size: 0.85rem;
  }
}

@media (max-width: 360px) {
  .contact-section {
    padding: 30px 5px;
  }

  .section-title {
    font-size: 2rem;
  }

  .info-card, .form-card {
    padding: 20px 12px;
  }

  .card-title {
    font-size: 1.4rem;
  }

  .contact-item {
    margin-bottom: 15px;
  }

  .contact-value {
    font-size: 0.85rem;
  }

  .form-input, .form-select, .form-textarea {
    padding: 8px 10px;
    font-size: 0.85rem;
  }

  .submit-btn {
    padding: 10px 18px;
    font-size: 0.85rem;
  }

  .cta-title {
    font-size: 1.5rem;
  }

  .info-item {
    padding: 18px 12px;
  }
}
</style>
