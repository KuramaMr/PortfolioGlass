<template>
  <nav class="glass-navbar">
    <div class="nav-container" ref="navContainer">
      <div
        class="nav-bubble"
        ref="bubble"
      >
        <div class="bubble-glow" ref="bubbleGlow"></div>
        <div class="bubble-ripple" ref="bubbleRipple"></div>
      </div>

      <ul class="nav-links">
        <li
          v-for="(link, index) in navLinks"
          :key="`nav-${link.name}-${index}`"
          class="nav-item"
          :ref="el => setLinkRef(el, index)"
          @mouseenter="() => onHover(index)"
          @mouseleave="onLeave"
          @mousedown="() => onPress()"
          @mouseup="onRelease"
          @click="() => onClick(index)"
        >
          <a
            href="#"
            class="nav-link"
            :class="{ active: activeIndex === index }"
            @click.prevent
          >
            {{ link.name }}
          </a>
        </li>
      </ul>
    </div>
  </nav>
</template>

<script setup>
import { ref, onMounted, nextTick, onUnmounted } from 'vue'
import { gsap } from 'gsap'

const navLinks = [
  { name: 'Accueil', href: '#home' },
  { name: 'Formations', href: '#formations' },
  { name: 'À propos', href: '#about' },
  { name: 'Contact', href: '#contact' }
]

const activeIndex = ref(0)
const currentHoveredIndex = ref(0)
const linkRefs = ref([])
const navContainer = ref(null)
const bubble = ref(null)
const bubbleGlow = ref(null)
const bubbleRipple = ref(null)

let mainTween = null
let glowTween = null
let isHovering = ref(false)
let scrollTimeout = null

// Fonction pour définir les refs des liens
const setLinkRef = (el, index) => {
  if (el) {
    linkRefs.value[index] = el
  }
}

// Fonction pour obtenir les refs des liens
const getLinkRef = (index) => {
  return linkRefs.value[index]
}

// Détection de section active via scroll
const detectActiveSection = () => {
  const sections = navLinks.map(link => document.querySelector(link.href)).filter(Boolean)
  const scrollPosition = window.scrollY + 100 // Offset pour tenir compte de la navbar

  let currentSection = 0

  sections.forEach((section, index) => {
    if (section.offsetTop <= scrollPosition) {
      currentSection = index
    }
  })

  // Toujours mettre à jour l'index actif
  if (activeIndex.value !== currentSection) {
    activeIndex.value = currentSection

    // Si on n'est pas en train de survoler, déplacer la bulle vers la section active
    if (!isHovering.value) {
      currentHoveredIndex.value = currentSection
      moveBubbleTo(currentSection, false)
    }
  }
}

const handleScroll = () => {
  if (scrollTimeout) {
    clearTimeout(scrollTimeout)
  }

  scrollTimeout = setTimeout(() => {
    detectActiveSection()
  }, 10) // Debounce léger pour les performances
}

const initBubbleAnimations = () => {
  // S'assurer que la bulle est visible
  gsap.set(bubble.value, {
    opacity: 1,
    visibility: 'visible'
  })

  // Glow de base très doux
  gsap.set(bubbleGlow.value, {
    scale: 1,
    opacity: 0.3
  })
}

const moveBubbleTo = (index, isClick = false) => {
  const targetLink = getLinkRef(index)
  if (!targetLink || !navContainer.value) return

  const containerRect = navContainer.value.getBoundingClientRect()
  const linkRect = targetLink.getBoundingClientRect()

  const offsetX = linkRect.left - containerRect.left
  const width = linkRect.width

  // Kill les animations précédentes pour éviter les conflits
  if (mainTween) mainTween.kill()
  if (glowTween) glowTween.kill()

  // Animation principale ultra-fluide
  const duration = isClick ? 0.6 : 0.3
  const ease = isClick ? "elastic.out(1, 0.4)" : "power2.out"

  mainTween = gsap.to(bubble.value, {
    x: offsetX,
    width: width,
    duration: duration,
    ease: ease,
    overwrite: "auto"
  })

  // Animation du glow synchronisée
  glowTween = gsap.to(bubbleGlow.value, {
    scale: isClick ? 1.2 : 1.1,
    opacity: isClick ? 0.5 : 0.4,
    duration: duration * 0.5,
    ease: "power2.out",
    yoyo: !isClick,
    repeat: isClick ? 0 : 1,
    overwrite: "auto"
  })
}

const onHover = (index) => {
  currentHoveredIndex.value = index
  isHovering.value = true
  moveBubbleTo(index, false)

  // Effet de loupe sur le lien survolé
  const targetLink = getLinkRef(index)
  if (targetLink) {
    gsap.to(targetLink, {
      scale: 1.1,
      duration: 0.3,
      ease: "back.out(1.7)",
      overwrite: "auto"
    })
  }
}

const onLeave = () => {
  isHovering.value = false

  // Remettre tous les liens à leur taille normale
  navLinks.forEach((_, index) => {
    const link = getLinkRef(index)
    if (link) {
      gsap.to(link, {
        scale: 1,
        duration: 0.3,
        ease: "back.out(1.7)",
        overwrite: "auto"
      })
    }
  })

  // Attendre un peu pour voir si on survole un autre élément
  gsap.delayedCall(0.1, () => {
    if (!isHovering.value) {
      currentHoveredIndex.value = activeIndex.value
      moveBubbleTo(activeIndex.value, false)
    }
  })
}

const onPress = () => {
  // Animation de pression rapide et subtile
  gsap.to(bubble.value, {
    scale: 0.96,
    duration: 0.1,
    ease: "power2.out",
    yoyo: true,
    repeat: 1,
    overwrite: "auto"
  })

  createRippleEffect()
}

const onRelease = () => {
  // Rien de spécial, l'animation de pression fait déjà le yoyo
}

const onClick = (index) => {
  activeIndex.value = index
  currentHoveredIndex.value = index
  isHovering.value = true

  // Effet de loupe prononcé au clic
  const targetLink = getLinkRef(index)
  if (targetLink) {
    gsap.timeline()
      .to(targetLink, {
        scale: 1.15,
        duration: 0.1,
        ease: "power2.out",
        overwrite: "auto"
      })
      .to(targetLink, {
        scale: 1.1,
        duration: 0.2,
        ease: "back.out(1.7)",
        overwrite: "auto"
      })
  }

  // Animation spéciale pour le clic
  moveBubbleTo(index, true)

  // Navigation vers la section correspondante
  const targetSection = navLinks[index].href
  if (targetSection && targetSection.startsWith('#')) {
    const element = document.querySelector(targetSection)
    if (element) {
      // Temporairement désactiver le listener de scroll pendant la navigation
      window.removeEventListener('scroll', handleScroll)

      element.scrollIntoView({ behavior: 'smooth' })

      // Réactiver le listener après la navigation
      setTimeout(() => {
        window.addEventListener('scroll', handleScroll, { passive: true })
        isHovering.value = false
      }, 1000)
    }
  }
}

const createRippleEffect = () => {
  // Reset et animation du ripple
  gsap.set(bubbleRipple.value, {
    scale: 0,
    opacity: 0.4
  })

  gsap.to(bubbleRipple.value, {
    scale: 1.8,
    opacity: 0,
    duration: 0.6,
    ease: "power2.out",
    overwrite: "auto"
  })
}

onMounted(async () => {
  await nextTick()

  // Animation d'entrée simple
  gsap.fromTo(".glass-navbar", {
    y: -50,
    opacity: 0
  }, {
    y: 0,
    opacity: 1,
    duration: 0.6,
    ease: "back.out(1.7)"
  })

  // Attendre que les éléments soient rendus
  setTimeout(() => {
    // Position initiale de la bulle sur le premier élément (par défaut)
    const firstLink = getLinkRef(0)
    if (firstLink && navContainer.value && bubble.value) {
      const containerRect = navContainer.value.getBoundingClientRect()
      const linkRect = firstLink.getBoundingClientRect()

      gsap.set(bubble.value, {
        x: linkRect.left - containerRect.left,
        width: linkRect.width,
        opacity: 1,
        visibility: 'visible'
      })
    }

    // Démarrer les animations de base
    initBubbleAnimations()

    // Ajouter le listener de scroll pour la détection de section active
    window.addEventListener('scroll', handleScroll, { passive: true })

    // Détecter la section active au chargement et ajuster la bulle si nécessaire
    setTimeout(() => {
      detectActiveSection()

      // Si la section active n'est pas la première, déplacer la bulle
      if (activeIndex.value !== 0) {
        moveBubbleTo(activeIndex.value, false)
      }
    }, 100)
  }, 200)
})

onUnmounted(() => {
  // Nettoyer toutes les animations GSAP
  gsap.killTweensOf([bubble.value, bubbleGlow.value, bubbleRipple.value])
  if (mainTween) mainTween.kill()
  if (glowTween) glowTween.kill()

  // Nettoyer les listeners
  window.removeEventListener('scroll', handleScroll)
  if (scrollTimeout) {
    clearTimeout(scrollTimeout)
  }
})
</script>

<style scoped>
.glass-navbar {
  position: fixed;
  top: 30px;
  left: 50%;
  transform: translateX(-50%);
  z-index: 1000;
  padding: 8px;
  background: rgba(255, 255, 255, 0.1);
  backdrop-filter: blur(20px);
  -webkit-backdrop-filter: blur(20px);
  border: 1px solid rgba(255, 255, 255, 0.2);
  border-radius: 50px;
  box-shadow:
    0 8px 32px rgba(0, 0, 0, 0.1),
    inset 0 1px 0 rgba(255, 255, 255, 0.2);
}

.nav-container {
  position: relative;
  display: flex;
  align-items: center;
}

.nav-bubble {
  position: absolute;
  top: 4px;
  left: 4px;
  height: calc(100% - 8px);
  width: 100px; /* Largeur par défaut pour que ce soit visible */
  background: rgba(255, 255, 255, 0.2);
  backdrop-filter: blur(15px);
  -webkit-backdrop-filter: blur(15px);
  border-radius: 25px;
  border: 1px solid rgba(255, 255, 255, 0.3);
  box-shadow:
    0 4px 16px rgba(0, 0, 0, 0.1),
    inset 0 1px 0 rgba(255, 255, 255, 0.2);
  pointer-events: none;
  overflow: hidden;
  will-change: transform, width;
  opacity: 1;
  visibility: visible;
}

.bubble-glow {
  position: absolute;
  top: -10%;
  left: -10%;
  width: 120%;
  height: 120%;
  background: radial-gradient(
    circle at 35% 25%,
    rgba(255, 255, 255, 0.15) 0%,
    rgba(255, 255, 255, 0.05) 40%,
    transparent 70%
  );
  border-radius: 50%;
  will-change: transform, opacity;
}

.bubble-ripple {
  position: absolute;
  top: 50%;
  left: 50%;
  width: 100%;
  height: 100%;
  background: radial-gradient(
    circle,
    rgba(255, 255, 255, 0.2) 0%,
    transparent 60%
  );
  border-radius: 50%;
  transform: translate(-50%, -50%);
  pointer-events: none;
  will-change: transform, opacity;
}

.nav-links {
  display: flex;
  list-style: none;
  margin: 0;
  padding: 0;
  gap: 10px;
  position: relative;
  z-index: 2;
}

.nav-item {
  position: relative;
  will-change: transform;
}

.nav-link {
  display: block;
  padding: 12px 20px;
  text-decoration: none;
  color: rgba(255, 255, 255, 0.9);
  font-weight: 500;
  font-size: 14px;
  border-radius: 25px;
  transition: color 0.3s ease, text-shadow 0.3s ease;
  position: relative;
  white-space: nowrap;
  background: transparent !important;
  border: none;
}

.nav-link:hover {
  color: rgba(255, 255, 255, 1);
  text-shadow: 0 0 10px rgba(255, 255, 255, 0.5);
  background: transparent !important;
}

.nav-link.active {
  color: rgba(255, 255, 255, 1);
  font-weight: 600;
  background: transparent !important;
  text-shadow: 0 0 15px rgba(255, 255, 255, 0.8);
}

/* Neutraliser les styles globaux */
.glass-navbar a {
  background: transparent !important;
  color: rgba(255, 255, 255, 0.9) !important;
  padding: 12px 20px !important;
}

.glass-navbar a:hover {
  background: transparent !important;
  color: rgba(255, 255, 255, 1) !important;
}

/* Responsive amélioré - desktop reste centré */
@media (max-width: 768px) {
  .glass-navbar {
    top: 15px;
    left: 15px;
    right: 15px;
    transform: none;
    width: calc(100% - 30px);
    padding: 5px;
  }

  .nav-link {
    padding: 10px 16px;
    font-size: 13px;
  }

  .nav-links {
    gap: 5px;
  }
}

@media (max-width: 480px) {
  .glass-navbar {
    top: 10px;
    left: 10px;
    right: 10px;
    width: calc(100% - 20px);
    padding: 4px;
    border-radius: 25px;
  }

  .nav-bubble {
    border-radius: 20px;
  }

  .nav-link {
    padding: 8px 10px;
    font-size: 11px;
    white-space: nowrap;
  }

  .nav-links {
    gap: 2px;
  }
}

@media (max-width: 410px) {
  .glass-navbar {
    top: 8px;
    left: 8px;
    right: 8px;
    width: calc(100% - 16px);
    padding: 3px;
  }

  .nav-link {
    padding: 6px 8px;
    font-size: 10px;
  }

  .nav-links {
    gap: 1px;
  }
}

@media (max-width: 360px) {
  .glass-navbar {
    top: 5px;
    left: 5px;
    right: 5px;
    width: calc(100% - 10px);
    padding: 2px;
  }

  .nav-link {
    padding: 5px 6px;
    font-size: 9px;
    letter-spacing: -0.2px;
  }

  .nav-links {
    gap: 0px;
  }
}

@media (max-width: 320px) {
  .glass-navbar {
    top: 3px;
    left: 3px;
    right: 3px;
    width: calc(100% - 6px);
    padding: 2px;
  }

  .nav-link {
    padding: 4px 5px;
    font-size: 8px;
    letter-spacing: -0.3px;
  }
}

/* Gestion de l'orientation paysage sur mobile */
@media (max-height: 500px) and (orientation: landscape) {
  .glass-navbar {
    top: 5px;
    padding: 3px;
  }

  .nav-link {
    padding: 6px 12px;
    font-size: 12px;
  }
}
</style>