<template>
  <q-page>
    
    <section id="home" class="portfolio-section bg-section-darker flex flex-center">
      <HeroSection />
    </section>

    <section id="about" class="portfolio-section bg-section-lighter flex flex-center">
      <AboutSection /> 
    </section>

    <section id="projects" class="portfolio-section bg-section-darker flex flex-center">
      <ProjectsSection />
    </section>

    <section id="experience" class="portfolio-section bg-section-lighter flex flex-center">
      <h2 class="text-white">Expérience</h2>
    </section>

  </q-page>
</template>

<script lang="ts" setup>
import { onMounted, onUnmounted } from 'vue'

import HeroSection from 'components/HeroSection.vue'
import AboutSection from 'components/AboutSection.vue'
import ProjectsSection from 'components/ProjectsSection.vue'

let observer: IntersectionObserver;

onMounted(() => {
  // Les marges définissent une zone de détection au milieu de l'écran (environ 40% de hauteur)
  const options = {
    root: null,
    rootMargin: '-30% 0px -30% 0px', 
    threshold: 0
  }

  observer = new IntersectionObserver((entries) => {
    entries.forEach((entry) => {
      // Si la section entre dans la zone de détection
      if (entry.isIntersecting) {
        window.dispatchEvent(new CustomEvent('section-changed', { detail: entry.target.id }))
      }
    })
  }, options)

  // Utiliser setTimeout pour s'assurer que le DOM est complètement rendu avant d'observer
  setTimeout(() => {
    document.querySelectorAll('section[id]').forEach((section) => {
      observer.observe(section)
    })
  }, 100)
})

onUnmounted(() => {
  if (observer) observer.disconnect()
})
</script>

<style>
/* --- Dans IndexPage.vue --- */

.bg-section-darker {
  background-color: #0B0E14;
}

.bg-section-lighter {
  /* On force la couleur de fond de base */
  background-color: #131821;
  
  /* TRANSITION ULTRA-FLUIDE */
  background-image: 
    /* 1. Le Halo "Vagrant" (Profondeur) en haut à droite */
    radial-gradient(circle at 85% 30%, rgba(124, 58, 237, 0.1) 0%, rgba(19, 24, 33, 0) 60%),
    /* 2. Le fondu : on commence par la couleur du Hero et on fond très lentement (40%) */
    linear-gradient(to bottom, #0B0E14 0%, #131821 40%);

  /* L'ARTILLERIE LOURDE : 
     On remonte la section de 50px pour qu'elle "morde" largement sur le Hero.
     On rajoute 50px de padding pour ne pas perdre d'espace en haut.
  */
  margin-top: -50px !important;
  padding-top: 50px !important;
  position: relative;
  z-index: 2;
}

.portfolio-section {
  width: 100%;
  min-height: 100vh;
  /* On s'assure qu'aucun débordement ne crée de scrollbar parasite */
  overflow: hidden; 
}
</style>