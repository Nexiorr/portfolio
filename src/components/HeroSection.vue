<template>
  <section id="home" class="full-height-section hero-glow flex">
    <div class="container-center">
      <div class="hero-content q-px-xl">
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
          <q-btn
            unelevated
            class="btn-purple"
            label="Mon CV"
            icon-right="file_download"
            no-caps
            padding="12px 24px"
            href="res/CV_Zhang_Dylan.pdf"
            target="_blank"
          />
        </div>
      </div>
    </div>
  </section>
</template>

<script lang="ts" setup>
import { onMounted } from 'vue'
import { animate, stagger } from 'motion'

onMounted(() => {
  animate(
    ".reveal-item",
    { opacity: [0, 1], y: [30, 0] },
    { delay: stagger(0.15), duration: 0.8, ease: "easeOut" }
  )
})
</script>

<style scoped>
.hero-glow {
  min-height: 100vh;
  width: 100%;
  background: radial-gradient(circle at 20% 70%, rgba(124, 58, 237, 0.08) 0%, #0B0E14 60%);
  padding-top: 10vh;
}

.hero-content {
  max-width: 900px;
  width: 100%;
  margin-left: 16%;
}

.text-purple-accent {
  color: #8B5CF6;
}

.btn-purple {
  background-color: #7C3AED;
  color: white;
  border-radius: 8px;
  font-weight: 600;
  transition: transform 0.3s cubic-bezier(0.175, 0.885, 0.32, 1.275), box-shadow 0.3s ease;
}

.btn-purple:hover {
  transform: translateY(-3px);
  box-shadow: 0 8px 20px rgba(124, 58, 237, 0.4);
}

.max-width-text {
  max-width: 650px;
  line-height: 1.6;
}
</style>
