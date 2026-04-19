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

const scrollTo = (sectionId: string) => {
  activeSection.value = sectionId
  const element = document.getElementById(sectionId)
  if (element) {
    element.scrollIntoView({ behavior: 'smooth' })
  }
}

const updateActiveSection = (event: CustomEvent) => {
  activeSection.value = event.detail
}

onMounted(() => {
  window.addEventListener('section-changed', updateActiveSection as EventListener)
})

onUnmounted(() => {
  window.removeEventListener('section-changed', updateActiveSection as EventListener)
})
</script>

<style>
.bg-primary-dark {
  background-color: #0B0E14;
}
.bg-sidebar {
  background-color: #05070A;
  border-right: 1px solid rgba(255, 255, 255, 0.05);
}

.nav-item {
  color: #8A92A3;
  transition: all 0.3s ease;
}
.nav-item:hover {
  background: rgba(255, 255, 255, 0.03);
  color: #FFFFFF;
}

.active-nav-item {
  background: rgba(124, 58, 237, 0.15) !important;
  color: #FFFFFF !important;
  border-left: 3px solid #7C3AED;
}
</style>
