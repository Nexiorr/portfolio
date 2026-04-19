<template>
  <q-page>

    <section id="home" class="portfolio-section bg-section-darker flex flex-center">
      <HeroSection />
    </section>

    <section id="about" class="portfolio-section bg-section-lighter flex flex-center">
      <AboutSection />
    </section>

    <section id="projects" class="portfolio-section bg-section-darker-transition flex flex-center">
      <ProjectsSection />
    </section>

    <section id="experience" class="portfolio-section bg-section-lighter-transition flex flex-center">
      <ExperienceSection />
    </section>

  </q-page>
</template>

<script lang="ts" setup>
import { onMounted, onUnmounted } from 'vue'

import HeroSection from 'components/HeroSection.vue'
import AboutSection from 'components/AboutSection.vue'
import ProjectsSection from 'components/ProjectsSection.vue'
import ExperienceSection from 'components/ExperienceSection.vue'

let observer: IntersectionObserver;

onMounted(() => {
  const options = {
    root: null,
    rootMargin: '-30% 0px -30% 0px',
    threshold: 0
  }

  observer = new IntersectionObserver((entries) => {
    entries.forEach((entry) => {
      if (entry.isIntersecting) {
        window.dispatchEvent(new CustomEvent('section-changed', { detail: entry.target.id }))
      }
    })
  }, options)

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

.bg-section-darker {
  background-color: #0B0E14;
}

.bg-section-darker-transition {
  background-color: #0B0E14;
  margin-top: -100px !important;
  padding-top: 100px !important;
  position: relative;
  z-index: 3;

  background-image: linear-gradient(to bottom, #131821 0%, #0B0E14 30%);
}

.bg-section-lighter {
  background-color: #131821;

  background-image:
    radial-gradient(circle at 85% 30%, rgba(124, 58, 237, 0.1) 0%, rgba(19, 24, 33, 0) 60%),
    linear-gradient(to bottom, #0B0E14 0%, #131821 40%);

  margin-top: -100px !important;
  padding-top: 100px !important;
  position: relative;
  z-index: 2;
}

.bg-section-lighter-transition {
  background-color: #131821;
  margin-top: -100px !important;
  padding-top: 100px !important;
  position: relative;
  z-index: 4;

  background-image: linear-gradient(to bottom, #0B0E14 0%, #131821 30%);
}

.portfolio-section {
  width: 100%;
  min-height: 100vh;
  overflow: hidden;
}

</style>
