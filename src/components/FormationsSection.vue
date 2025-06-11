<template>
  <section id="formations" class="formations-section">
    <div class="container">
      <div class="section-header">
        <h2 class="section-title">Mes Formations CACES</h2>
        <p class="section-subtitle">
          Lorem ipsum dolor sit amet, consectetur adipiscing elit.
          Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
        </p>
      </div>

      <div class="formations-grid">
        <div
          v-for="formation in formations"
          :key="formation.id"
          class="formation-card"
          @click="openFormationDetail(formation)"
        >
          <div class="card-icon">
            <component :is="formation.icon" />
          </div>

          <h3 class="card-title">{{ formation.title }}</h3>
          <p class="card-description">{{ formation.description }}</p>

          <div class="card-details">
            <div class="detail-item">
              <span class="detail-label">Durée :</span>
              <span class="detail-value">{{ formation.duration }}</span>
            </div>
            <div class="detail-item">
              <span class="detail-label">Validité :</span>
              <span class="detail-value">{{ formation.validity }}</span>
            </div>
          </div>

          <div class="card-badges">
            <span
              v-for="badge in formation.badges"
              :key="badge"
              class="badge"
            >
              {{ badge }}
            </span>
          </div>

          <div class="card-action">
            <button class="detail-btn">
              Voir les détails
              <svg width="16" height="16" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
                <path d="M12 4l-1.41 1.41L16.17 11H4v2h12.17l-5.58 5.59L12 20l8-8z" fill="currentColor"/>
              </svg>
            </button>
          </div>
        </div>
      </div>

      <div class="certifications-section">
        <h3 class="certifications-title">Certifications & Agréments</h3>
        <div class="certifications-grid">
          <div
            v-for="cert in certifications"
            :key="cert.id"
            class="certification-card"
          >
            <div class="cert-icon">{{ cert.icon }}</div>
            <div class="cert-content">
              <h4 class="cert-title">{{ cert.title }}</h4>
              <p class="cert-description">{{ cert.description }}</p>
            </div>
          </div>
        </div>
      </div>
    </div>

    <!-- Modal de détail de formation -->
    <FormationDetail
      :formation="selectedFormation"
      :isVisible="isDetailVisible"
      @close="closeFormationDetail"
    />
  </section>
</template>

<script setup>
import { ref, markRaw } from 'vue'
import FormationDetail from './FormationDetail.vue'

// Icônes SVG simplifiées avec markRaw
const TruckIcon = markRaw({
  template: `
    <svg width="40" height="40" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
      <path d="M3 17h2l.5-2h13l.5 2h2v-4h-3V9H6v4H3v4zm3-6h10v2H6v-2z" fill="rgba(255,255,255,0.8)"/>
    </svg>
  `
})

const CraneIcon = markRaw({
  template: `
    <svg width="40" height="40" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
      <path d="M2 19h20v2H2v-2zm1.5-6.5L5 11l1.5 1.5L8 11l1.5 1.5L11 11l1.5 1.5L14 11l1.5 1.5L17 11l1.5 1.5L20 11v7H4v-5.5z" fill="rgba(255,255,255,0.8)"/>
    </svg>
  `
})

const ForkliftIcon = markRaw({
  template: `
    <svg width="40" height="40" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
      <path d="M6 17c1.1 0 2-.9 2-2s-.9-2-2-2-2 .9-2 2 .9 2 2 2zm10 0c1.1 0 2-.9 2-2s-.9-2-2-2-2 .9-2 2 .9 2 2 2zM3 7h14l-1 5H6L3 7z" fill="rgba(255,255,255,0.8)"/>
    </svg>
  `
})

const PlatformIcon = markRaw({
  template: `
    <svg width="40" height="40" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
      <path d="M4 4h16v2H4V4zm0 4h16v12H4V8zm2 2v8h12v-8H6z" fill="rgba(255,255,255,0.8)"/>
    </svg>
  `
})

// État pour la modal de détail
const selectedFormation = ref(null)
const isDetailVisible = ref(false)

const openFormationDetail = (formation) => {
  selectedFormation.value = formation
  isDetailVisible.value = true
}

const closeFormationDetail = () => {
  isDetailVisible.value = false
  selectedFormation.value = null
}

const formations = ref([
  {
    id: 1,
    title: 'CACES R489 - Chariots élévateurs',
    description: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Formation complète pour la conduite de chariots élévateurs en sécurité.',
    duration: '2-3 jours',
    validity: '5 ans',
    price: '480€ - 650€',
    maxParticipants: '8 personnes',
    icon: ForkliftIcon,
    badges: ['Cat. 1A', 'Cat. 3', 'Cat. 5'],
    categories: [
      {
        name: 'Catégorie 1A',
        description: 'Transpalettes à conducteur porté et préparateurs de commandes au sol',
        engins: ['Transpalette électrique', 'Préparateur de commandes']
      },
      {
        name: 'Catégorie 3',
        description: 'Chariots élévateurs en porte-à-faux à conducteur assis',
        engins: ['Chariot frontal', 'Chariot électrique']
      },
      {
        name: 'Catégorie 5',
        description: 'Chariots élévateurs à mât rétractable à conducteur assis',
        engins: ['Chariot à mât rétractable', 'Reach truck']
      }
    ],
    program: [
      {
        title: 'Accueil et présentation',
        description: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Présentation des objectifs et du déroulement de la formation.',
        duration: '30 min'
      },
      {
        title: 'Réglementation et responsabilités',
        description: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Étude des textes réglementaires et des responsabilités.',
        duration: '2h'
      },
      {
        title: 'Technologie des chariots',
        description: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Fonctionnement, organes de sécurité, maintenance.',
        duration: '3h'
      },
      {
        title: 'Conduite et manœuvres',
        description: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Apprentissage pratique de la conduite en sécurité.',
        duration: '8h'
      },
      {
        title: 'Évaluation finale',
        description: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Test théorique et pratique.',
        duration: '2h'
      }
    ],
    prerequisites: [
      'Être âgé de 18 ans minimum',
      'Maîtriser la langue française (oral et écrit)',
      'Avoir une aptitude médicale au poste de travail',
      'Posséder les EPI obligatoires'
    ],
    requiredDocuments: [
      'Pièce d\'identité en cours de validité',
      'Certificat médical d\'aptitude',
      'Attestation de formation aux premiers secours',
      'Autorisation de conduite de l\'employeur'
    ],
    medicalRequirements: [
      'Acuité visuelle suffisante',
      'Absence de troubles de l\'équilibre',
      'Capacité de réaction appropriée',
      'Absence de consommation de substances'
    ],
    theoreticalTest: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. QCM de 40 questions portant sur la réglementation, la technologie et la sécurité.',
    practicalTest: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Épreuve pratique de conduite avec différents exercices de manutention et circulation.',
    certification: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Délivrance du CACES R489 valable 5 ans sur présentation de l\'autorisation de conduite.'
  },
  {
    id: 2,
    title: 'CACES R482 - Engins de chantier',
    description: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Formation aux engins de terrassement et de manutention.',
    duration: '3-5 jours',
    validity: '10 ans',
    price: '750€ - 1200€',
    maxParticipants: '6 personnes',
    icon: TruckIcon,
    badges: ['Cat. A', 'Cat. B1', 'Cat. C1'],
    categories: [
      {
        name: 'Catégorie A',
        description: 'Engins compacts (masse ≤ 6 tonnes)',
        engins: ['Mini-pelle', 'Mini-chargeur', 'Dumper']
      },
      {
        name: 'Catégorie B1',
        description: 'Engins d\'extraction et de chargement à déplacement séquentiel',
        engins: ['Pelle hydraulique', 'Pelle de manutention']
      },
      {
        name: 'Catégorie C1',
        description: 'Engins de chargement à déplacement alternatif',
        engins: ['Chargeuse sur pneus', 'Chargeuse-pelleteuse']
      }
    ],
    program: [
      {
        title: 'Réglementation des engins de chantier',
        description: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Cadre réglementaire et responsabilités.',
        duration: '2h'
      },
      {
        title: 'Technologie et maintenance',
        description: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Fonctionnement des engins et maintenance préventive.',
        duration: '4h'
      },
      {
        title: 'Sécurité sur chantier',
        description: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Règles de sécurité et de circulation.',
        duration: '3h'
      },
      {
        title: 'Conduite pratique',
        description: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Apprentissage de la conduite et des manœuvres.',
        duration: '12h'
      },
      {
        title: 'Évaluations',
        description: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Tests théorique et pratique.',
        duration: '3h'
      }
    ],
    prerequisites: [
      'Être âgé de 18 ans minimum',
      'Aptitude médicale à la conduite d\'engins',
      'Maîtriser les savoirs de base',
      'Formation aux risques du BTP'
    ],
    requiredDocuments: [
      'Pièce d\'identité',
      'Certificat médical spécialisé',
      'Attestation de compétences de base',
      'Équipements de protection individuelle'
    ],
    medicalRequirements: [
      'Visite médicale spécialisée BTP',
      'Absence de contre-indications',
      'Capacités physiques adaptées',
      'Acuité auditive et visuelle'
    ],
    theoreticalTest: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Épreuve théorique sur la réglementation et la technologie des engins.',
    practicalTest: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Épreuve pratique avec exercices de conduite et de manutention spécifiques.',
    certification: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. CACES R482 valable 10 ans avec renouvellement obligatoire.'
  },
  {
    id: 3,
    title: 'CACES R487 - Grues mobiles',
    description: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Formation pour la conduite de grues mobiles automotrices.',
    duration: '5 jours',
    validity: '5 ans',
    price: '1200€ - 1800€',
    maxParticipants: '4 personnes',
    icon: CraneIcon,
    badges: ['Cat. 1', 'Cat. 2'],
    categories: [
      {
        name: 'Catégorie 1',
        description: 'Grues mobiles de 20 tonnes maximum',
        engins: ['Grue mobile légère', 'Grue automotrice']
      },
      {
        name: 'Catégorie 2',
        description: 'Grues mobiles de plus de 20 tonnes',
        engins: ['Grue mobile lourde', 'Grue tout terrain']
      }
    ],
    program: [
      {
        title: 'Réglementation grues mobiles',
        description: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Cadre légal et normes de sécurité.',
        duration: '3h'
      },
      {
        title: 'Technologie des grues',
        description: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Systèmes hydrauliques, électroniques et mécaniques.',
        duration: '6h'
      },
      {
        title: 'Calculs de charge et stabilité',
        description: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Abaques, calculs de moment et stabilité.',
        duration: '4h'
      },
      {
        title: 'Conduite et grutage',
        description: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Techniques de grutage et manœuvres complexes.',
        duration: '15h'
      },
      {
        title: 'Évaluation complète',
        description: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Tests théorique et pratique approfondis.',
        duration: '4h'
      }
    ],
    prerequisites: [
      'Permis poids lourd en cours de validité',
      'Expérience en manutention recommandée',
      'Aptitude médicale spécifique',
      'Formation sécurité obligatoire'
    ],
    requiredDocuments: [
      'Permis de conduire C ou CE',
      'Certificat médical grue mobile',
      'Attestation formation sécurité',
      'Casque et chaussures de sécurité'
    ],
    medicalRequirements: [
      'Visite médicale grue mobile',
      'Tests psychotechniques',
      'Absence de vertiges',
      'Excellente coordination'
    ],
    theoreticalTest: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. QCM spécialisé sur la technologie des grues et les calculs de charge.',
    practicalTest: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Épreuve pratique complexe avec exercices de grutage variés.',
    certification: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. CACES R487 valable 5 ans, renouvelable après formation de recyclage.'
  },
  {
    id: 4,
    title: 'CACES R486 - PEMP',
    description: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Formation aux plateformes élévatrices mobiles de personnes.',
    duration: '2-3 jours',
    validity: '5 ans',
    price: '550€ - 750€',
    maxParticipants: '8 personnes',
    icon: PlatformIcon,
    badges: ['Cat. A', 'Cat. B'],
    categories: [
      {
        name: 'Catégorie A',
        description: 'PEMP verticales (élévation verticale)',
        engins: ['Nacelle ciseaux', 'Mât vertical']
      },
      {
        name: 'Catégorie B',
        description: 'PEMP multidirectionnelles (bras articulé/télescopique)',
        engins: ['Nacelle articulée', 'Nacelle télescopique']
      }
    ],
    program: [
      {
        title: 'Réglementation PEMP',
        description: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Cadre réglementaire et obligations.',
        duration: '2h'
      },
      {
        title: 'Technologie des PEMP',
        description: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Fonctionnement et systèmes de sécurité.',
        duration: '3h'
      },
      {
        title: 'Sécurité et prévention',
        description: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Risques et mesures de prévention.',
        duration: '2h'
      },
      {
        title: 'Conduite et manœuvres',
        description: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Apprentissage pratique de la conduite.',
        duration: '6h'
      },
      {
        title: 'Évaluation',
        description: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Tests final théorique et pratique.',
        duration: '2h'
      }
    ],
    prerequisites: [
      'Être âgé de 18 ans minimum',
      'Aptitude au travail en hauteur',
      'Absence de vertige',
      'Formation EPI obligatoire'
    ],
    requiredDocuments: [
      'Pièce d\'identité valide',
      'Certificat médical travail en hauteur',
      'Attestation port du harnais',
      'Équipements de protection'
    ],
    medicalRequirements: [
      'Aptitude travail en hauteur',
      'Absence de troubles visuels',
      'Équilibre et coordination',
      'Résistance au stress'
    ],
    theoreticalTest: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Test sur la réglementation et la sécurité des PEMP.',
    practicalTest: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Épreuve pratique de conduite et positionnement en sécurité.',
    certification: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. CACES R486 valable 5 ans avec contrôle médical régulier.'
  }
])

const certifications = ref([
  {
    id: 1,
    title: 'Organisme Testeur Certifié',
    description: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit.',
    icon: '🏆'
  },
  {
    id: 2,
    title: 'Formateur Agréé INRS',
    description: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit.',
    icon: '📋'
  },
  {
    id: 3,
    title: 'Certification Qualité',
    description: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit.',
    icon: '⭐'
  }
])
</script>

<style scoped>
.formations-section {
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

.formations-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 30px;
  margin-bottom: 80px;
}

.formation-card {
  background: rgba(255, 255, 255, 0.1);
  backdrop-filter: blur(20px);
  -webkit-backdrop-filter: blur(20px);
  border: 1px solid rgba(255, 255, 255, 0.2);
  border-radius: 25px;
  padding: 40px 30px;
  box-shadow:
    0 20px 60px rgba(0, 0, 0, 0.1),
    inset 0 1px 0 rgba(255, 255, 255, 0.2);
  position: relative;
  overflow: hidden;
  transition: all 0.3s ease;
  cursor: pointer;
}

.formation-card:hover {
  transform: translateY(-5px);
  box-shadow:
    0 25px 70px rgba(0, 0, 0, 0.15),
    inset 0 1px 0 rgba(255, 255, 255, 0.2);
}

.formation-card::before {
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

.card-icon {
  text-align: center;
  margin-bottom: 25px;
  position: relative;
  z-index: 1;
}

.card-title {
  font-size: 1.4rem;
  font-weight: 600;
  color: rgba(255, 255, 255, 0.95);
  margin-bottom: 15px;
  text-align: center;
}

.card-description {
  color: rgba(255, 255, 255, 0.8);
  line-height: 1.6;
  margin-bottom: 25px;
  text-align: center;
}

.card-details {
  margin-bottom: 25px;
}

.detail-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 10px;
  padding: 8px 0;
  border-bottom: 1px solid rgba(255, 255, 255, 0.1);
}

.detail-label {
  color: rgba(255, 255, 255, 0.7);
  font-weight: 500;
}

.detail-value {
  color: rgba(255, 255, 255, 0.9);
  font-weight: 600;
}

.card-badges {
  display: flex;
  flex-wrap: wrap;
  gap: 8px;
  justify-content: center;
  margin-bottom: 25px;
}

.badge {
  background: rgba(255, 255, 255, 0.15);
  color: rgba(255, 255, 255, 0.9);
  padding: 5px 12px;
  border-radius: 12px;
  font-size: 0.8rem;
  font-weight: 500;
  border: 1px solid rgba(255, 255, 255, 0.2);
}

.card-action {
  text-align: center;
  position: relative;
  z-index: 1;
}

.detail-btn {
  background: rgba(255, 255, 255, 0.15);
  color: rgba(255, 255, 255, 0.9);
  border: 1px solid rgba(255, 255, 255, 0.3);
  border-radius: 50px;
  padding: 10px 20px;
  font-size: 0.9rem;
  font-weight: 500;
  cursor: pointer;
  transition: all 0.3s ease;
  display: flex;
  align-items: center;
  gap: 8px;
  margin: 0 auto;
  width: fit-content;
}

.detail-btn:hover {
  background: rgba(255, 255, 255, 0.2);
  transform: translateY(-2px);
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);
}

.certifications-section {
  text-align: center;
}

.certifications-title {
  font-size: 2.5rem;
  font-weight: 700;
  color: rgba(255, 255, 255, 0.95);
  margin-bottom: 40px;
  text-shadow: 0 2px 10px rgba(0, 0, 0, 0.3);
}

.certifications-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 25px;
}

.certification-card {
  background: rgba(255, 255, 255, 0.08);
  backdrop-filter: blur(15px);
  border: 1px solid rgba(255, 255, 255, 0.15);
  border-radius: 20px;
  padding: 25px;
  display: flex;
  align-items: center;
  gap: 15px;
  transition: all 0.3s ease;
}

.certification-card:hover {
  background: rgba(255, 255, 255, 0.12);
  transform: translateY(-2px);
}

.cert-icon {
  font-size: 2rem;
  background: rgba(255, 255, 255, 0.1);
  width: 60px;
  height: 60px;
  border-radius: 15px;
  display: flex;
  align-items: center;
  justify-content: center;
  border: 1px solid rgba(255, 255, 255, 0.2);
}

.cert-content {
  text-align: left;
  flex: 1;
}

.cert-title {
  font-size: 1.1rem;
  font-weight: 600;
  color: rgba(255, 255, 255, 0.95);
  margin-bottom: 5px;
}

.cert-description {
  color: rgba(255, 255, 255, 0.7);
  font-size: 0.9rem;
  line-height: 1.4;
}

@media (max-width: 1200px) {
  .formations-grid {
    grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
    gap: 25px;
  }
}

@media (max-width: 1024px) {
  .formations-section {
    padding: 60px 15px;
  }

  .section-title {
    font-size: 2.8rem;
  }

  .formations-grid {
    grid-template-columns: repeat(2, 1fr);
    gap: 20px;
  }

  .formation-card {
    padding: 35px 25px;
  }

  .certifications-grid {
    grid-template-columns: repeat(2, 1fr);
    gap: 20px;
  }
}

@media (max-width: 768px) {
  .formations-section {
    padding: 50px 10px;
  }

  .section-title {
    font-size: 2.5rem;
  }

  .section-subtitle {
    font-size: 1.1rem;
  }

  .formations-grid {
    grid-template-columns: 1fr;
    gap: 20px;
  }

  .formation-card {
    padding: 30px 20px;
  }

  .card-title {
    font-size: 1.3rem;
  }

  .card-description {
    font-size: 0.95rem;
  }

  .certifications-title {
    font-size: 2.2rem;
  }

  .certifications-grid {
    grid-template-columns: 1fr;
    gap: 15px;
  }

  .certification-card {
    text-align: center;
    flex-direction: column;
    padding: 20px;
  }

  .cert-content {
    text-align: center;
  }
}

@media (max-width: 480px) {
  .formations-section {
    padding: 40px 8px;
  }

  .section-title {
    font-size: 2.2rem;
  }

  .section-subtitle {
    font-size: 1rem;
    padding: 0 10px;
  }

  .formation-card {
    padding: 25px 15px;
    border-radius: 20px;
  }

  .card-title {
    font-size: 1.2rem;
    margin-bottom: 12px;
  }

  .card-description {
    font-size: 0.9rem;
    margin-bottom: 20px;
  }

  .detail-item {
    padding: 6px 0;
  }

  .detail-label, .detail-value {
    font-size: 0.9rem;
  }

  .badge {
    padding: 4px 8px;
    font-size: 0.75rem;
  }

  .detail-btn {
    padding: 8px 16px;
    font-size: 0.85rem;
  }

  .certifications-title {
    font-size: 2rem;
  }

  .certification-card {
    padding: 15px;
  }

  .cert-icon {
    width: 50px;
    height: 50px;
    font-size: 1.8rem;
  }

  .cert-title {
    font-size: 1rem;
  }

  .cert-description {
    font-size: 0.85rem;
  }
}

@media (max-width: 360px) {
  .formations-section {
    padding: 30px 5px;
  }

  .section-title {
    font-size: 2rem;
  }

  .formation-card {
    padding: 20px 12px;
  }

  .card-title {
    font-size: 1.1rem;
  }

  .badge {
    padding: 3px 6px;
    font-size: 0.7rem;
  }
}
</style>
