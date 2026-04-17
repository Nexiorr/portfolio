<template>
  <section id="home" class="full-height-section hero-glow flex">
    <div class="container-center">
      <div class="hero-content q-px-xl">
        
        <div class="badge-available q-mb-xl reveal-item">
          <q-icon name="auto_awesome" size="sm" class="q-mr-sm text-white" />
          <span class="text-white text-weight-medium">Available for opportunities</span>
        </div>

        <h1 class="text-h2 text-weight-bold text-white q-mb-sm reveal-item">
          Dylan Zhang
        </h1>
        <h2 class="text-h3 text-weight-bold text-purple-accent q-mb-md reveal-item q-mt-none">
          Future développeur full-stack.
        </h2>
        
        <p class="text-grey-5 text-h6 q-mt-lg max-width-text reveal-item">
          Passionné par la création d'expériences utilisateur exceptionnelles grâce à un code propre et un design réfléchi.
        </p>

        <div class="q-mt-xl q-gutter-md reveal-item">
          <q-btn unelevated class="btn-purple" label="View My Work" icon-right="arrow_forward" no-caps padding="12px 24px" />
          <q-btn outline color="white" label="Get In Touch" no-caps padding="12px 24px" />
        </div>
      </div>
    </div>
  </section>
</template>

<script lang="ts" setup>
import { onMounted } from 'vue'
import { animate, stagger } from 'motion'

onMounted(() => {
  // Animation d'apparition en cascade (plus propre que l'ancien code)
  animate(
    ".reveal-item", 
    { opacity: [0, 1], y: [30, 0] }, 
    { delay: stagger(0.15), duration: 0.8, ease: "easeOut" }
  )
})
</script>

<style scoped>
/* 1. L'EFFET "VAGRANT" (Le halo subtil) */
.hero-glow {
  min-height: 100vh;
  width: 100%;
  /* Un halo violet très transparent centré à gauche, qui fond vers le noir profond */
  background: radial-gradient(circle at 20% 70%, rgba(124, 58, 237, 0.08) 0%, #0B0E14 60%);
  padding-top: 10vh;
}

.hero-content {
  max-width: 900px;
  width: 100%;
  margin-left: 16%;
}

/* Le texte violet */
.text-purple-accent {
  color: #8B5CF6; /* Violet moderne */
}

/* Le style du badge */
.badge-available {
  background: rgba(255, 255, 255, 0.05);
  border: 1px solid rgba(255, 255, 255, 0.1);
  padding: 8px 20px;
  border-radius: 30px;
  display: inline-flex;
  align-items: center;
  font-size: 0.95rem;
}

/* Le bouton principal */
.btn-purple {
  background-color: #7C3AED;
  color: white;
  border-radius: 8px;
  font-weight: 600;
}

.max-width-text {
  max-width: 650px;
  line-height: 1.6;
}
</style>