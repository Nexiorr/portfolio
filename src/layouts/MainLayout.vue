<template>
  <q-layout view="hHh Lpr lFf" class="bg-primary-dark text-white">

    <q-header transparent class="lt-md">
      <q-toolbar>
        <q-btn flat dense round icon="menu" aria-label="Menu" @click="toggleLeftDrawer" />
      </q-toolbar>
    </q-header>

    <q-drawer
      v-model="leftDrawerOpen"
      show-if-above
      :width="260"

      :breakpoint="1024"
      class="bg-sidebar"
    >
      <div class="q-pa-lg full-height flex column">

        <div class="text-h6 text-weight-bold q-mb-xl q-mt-md">
          Dylan Zhang
        </div>

        <q-list class="nav-list q-gutter-y-sm">
          <q-item
            clickable
            v-ripple
            active-class="active-nav-item"
            :active="activeSection === 'home'"
            @click="scrollTo('home')"
            class="nav-item rounded-borders"
          >
            <q-item-section avatar min-width="40px">
              <q-icon name="home" size="sm" />
            </q-item-section>
            <q-item-section class="text-subtitle2 text-weight-medium">Home</q-item-section>
          </q-item>

          <q-item
            clickable
            v-ripple
            active-class="active-nav-item"
            :active="activeSection === 'about'"
            @click="scrollTo('about')"
            class="nav-item rounded-borders"
          >
            <q-item-section avatar min-width="40px">
              <q-icon name="person_outline" size="sm" />
            </q-item-section>
            <q-item-section class="text-subtitle2 text-weight-medium">About</q-item-section>
          </q-item>

          <q-item
            clickable
            v-ripple
            active-class="active-nav-item"
            :active="activeSection === 'projects'"
            @click="scrollTo('projects')"
            class="nav-item rounded-borders"
          >
            <q-item-section avatar min-width="40px">
              <q-icon name="code" size="sm" />
            </q-item-section>
            <q-item-section class="text-subtitle2 text-weight-medium">Projects</q-item-section>
          </q-item>

          <q-item
            clickable
            v-ripple
            active-class="active-nav-item"
            :active="activeSection === 'experience'"
            @click="scrollTo('experience')"
            class="nav-item rounded-borders"
          >
            <q-item-section avatar min-width="40px">
              <q-icon name="work_outline" size="sm" />
            </q-item-section>
            <q-item-section class="text-subtitle2 text-weight-medium">Experience</q-item-section>
          </q-item>
        </q-list>
      </div>
    </q-drawer>

    <q-page-container>
      <router-view />
    </q-page-container>

  </q-layout>
</template>

<script lang="ts" setup>
import { ref, onMounted, onUnmounted } from 'vue'

const leftDrawerOpen = ref(false)
const activeSection = ref('home')

const toggleLeftDrawer = () => {
  leftDrawerOpen.value = !leftDrawerOpen.value
}

// 1. Fonction pour faire défiler la page quand on clique sur le menu
const scrollTo = (sectionId: string) => {
  activeSection.value = sectionId
  const element = document.getElementById(sectionId)
  if (element) {
    element.scrollIntoView({ behavior: 'smooth' })
  }
}

// 2. Écouter le scroll de l'utilisateur pour mettre à jour le menu actif
const updateActiveSection = (event: CustomEvent) => {
  activeSection.value = event.detail
}

onMounted(() => {
  // On écoute l'événement envoyé par IndexPage.vue
  window.addEventListener('section-changed', updateActiveSection as EventListener)
})

onUnmounted(() => {
  // Toujours nettoyer les écouteurs d'événements
  window.removeEventListener('section-changed', updateActiveSection as EventListener)
})
</script>

<style>
/* Les couleurs exactes de ton screenshot */
.bg-primary-dark {
  background-color: #0B0E14; /* Couleur de fond principale */
}
.bg-sidebar {
  background-color: #05070A; /* Couleur de la sidebar (légèrement plus foncée) */
  border-right: 1px solid rgba(255, 255, 255, 0.05); /* Petite bordure discrète */
}

/* Style des liens du menu */
.nav-item {
  color: #8A92A3;
  transition: all 0.3s ease;
}
.nav-item:hover {
  background: rgba(255, 255, 255, 0.03);
  color: #FFFFFF;
}

/* Le style du bouton actif (Le bleu/violet de "Home" sur ton screen) */
.active-nav-item {
  background: rgba(124, 58, 237, 0.15) !important; /* Fond violet très transparent */
  color: #FFFFFF !important;
  border-left: 3px solid #7C3AED; /* La petite barre de sélection à gauche */
}
</style>
