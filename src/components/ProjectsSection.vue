<template>
  <div class="container-center q-px-xl full-width text-left" style="max-width: 1350px; margin: 0 auto;">
    
    <div class="flex items-center q-mb-md">
      <div class="section-badge q-mr-md">
        <q-icon name="code" size="xs" class="q-mr-xs" />
        <span>Portfolio</span>
      </div>
      <h3 class="text-h3 text-weight-bold text-white q-my-none">Projects & Case Studies</h3>
    </div>
    <p class="text-grey-5 text-h6 text-weight-light q-mb-xl max-width-text">
      Une vitrine de mes travaux récents, du concept au déploiement.
    </p>

    <div class="flex q-gutter-sm q-mb-xl">
      <q-btn 
        v-for="cat in categories" :key="cat"
        unelevated
        no-caps 
        :label="cat" 
        @click="currentCategory = cat"
        :class="currentCategory === cat ? 'btn-filter-active' : 'btn-filter-inactive'"
      />
    </div>

    <div class="row q-col-gutter-xl items-stretch">
      <div 
        v-for="project in filteredProjects" :key="project.id" 
        class="col-12 col-sm-6 col-md-4"
      >
        <q-card 
          class="project-card bg-card-dark no-shadow overflow-hidden full-height flex column"
          :style="{ '--brand-color': project.brandColor }"
        >
          
          <div class="image-wrapper">
             <q-img :src="project.image" class="project-image full-height" />
          </div>

          <q-card-section class="col-grow flex column q-pa-lg">
            
            <div class="title-container flex justify-between items-start q-mb-sm">
              <div class="text-h6 text-white text-weight-bold project-title-transition title-text">
                {{ project.title }}
              </div>
              <div class="text-caption text-grey-6 font-mono q-pt-xs">{{ project.year }}</div>
            </div>
            
            <p class="text-grey-5 text-body2 q-mb-md ellipsis-3-lines line-height-relaxed description-fixed-height">
              {{ project.description }}
            </p>

            <q-space /> <div class="flex q-gutter-xs q-mb-sm tags-container">
              <q-chip 
                v-for="tech in project.technologies" :key="tech"
                dense
                :ripple="false"
                class="chip-tech-da no-margin"
              >
                {{ tech }}
              </q-chip>
            </div>
          </q-card-section>

          <q-card-actions class="q-pa-lg q-pt-none q-gutter-sm row">
            <div class="col">
              <q-btn 
                outline 
                no-caps 
                label="Détails" 
                class="full-width btn-action-outline" 
                @click="openDetails(project)"
              />
            </div>
            <div class="col">
              <q-btn 
                outline 
                no-caps 
                label="View Live" 
                icon-right="launch"
                class="full-width btn-action-outline" 
              />
            </div>
          </q-card-actions>
        </q-card>
      </div>
    </div>

    <q-dialog v-model="detailsOpen" backdrop-filter="blur(8px) brightness(30%)">
      <q-card class="modal-dark-tech text-white" style="width: 850px; max-width: 95vw;">
        
        <q-card-section class="row items-center q-pa-lg bg-header-modal">
          <div class="text-h5 text-weight-bold">{{ selectedProject?.title }}</div>
          <q-space />
          <q-btn icon="close" flat round dense v-close-popup class="text-grey-5" />
        </q-card-section>

        <q-separator dark />

        <q-card-section class="q-pa-xl scroll modal-body-scroll">
          <div class="row q-col-gutter-xl">
            <div class="col-12 col-md-6 text-center">
              <q-img :src="selectedProject?.image" class="rounded-borders shadow-24 border-glass" :ratio="16/9" />
              <div class="q-mt-lg flex q-gutter-sm justify-center">
                <q-btn outline color="white" label="Live Demo" icon="launch" no-caps class="rounded-borders" />
                <q-btn outline color="white" label="Code" icon="code" no-caps class="rounded-borders" />
              </div>
            </div>

            <div class="col-12 col-md-6">
              <div class="q-mb-xl">
                <h6 class="text-subtitle1 text-weight-bold text-white flex items-center q-mb-md">
                  <q-icon name="work_outline" color="purple-4" size="xs" class="q-mr-sm"/>
                  VALORISATION DE L'EXPÉRIENCE (Point 2)
                </h6>
                <div class="q-mb-md">
                  <div class="text-purple-3 text-weight-bold text-uppercase text-caption q-mb-xs">Mon Rôle & Autonomie</div>
                  <div class="text-body2 text-grey-4 line-height-relaxed">{{ selectedProject?.role }}</div>
                </div>
                <div class="q-mb-md">
                  <div class="text-purple-3 text-weight-bold text-uppercase text-caption q-mb-xs">Interactions Équipe</div>
                  <div class="text-body2 text-grey-4 line-height-relaxed">{{ selectedProject?.interactions }}</div>
                </div>
              </div>

              <q-separator dark class="q-mb-xl" />

              <div>
                <h6 class="text-subtitle1 text-weight-bold text-white flex items-center q-mb-md">
                  <q-icon name="psychology" color="purple-4" size="xs" class="q-mr-sm"/>
                  ANALYSE RÉFLEXIVE (Point 5)
                </h6>
                <div class="text-body2 text-grey-4 line-height-relaxed italic border-left-purple q-pl-md q-py-xs">
                  "{{ selectedProject?.reflexive }}"
                </div>
              </div>
            </div>
          </div>
        </q-card-section>
      </q-card>
    </q-dialog>

  </div>
</template>

<script lang="ts" setup>
import { ref, computed } from 'vue'

interface Project {
  id: number
  title: string
  category: string
  description: string
  image: string
  year: number
  technologies: string[]
  brandColor: string
  role: string
  interactions: string
  reflexive: string
}

const currentCategory = ref('All')
const categories = ['All', 'Web', 'Mobile', 'Fullstack', 'Design']
const detailsOpen = ref(false)
const selectedProject = ref<Project | null>(null)

// Données
const projects = ref<Project[]>([
  {
    id: 1,
    title: 'Knest – AI Second Brain',
    category: 'Fullstack',
    brandColor: '#A855F7', 
    description: 'Une application de gestion de connaissances utilisant l\'IA pour connecter des notes et automatiser l\'organisation.',
    image: 'https://cdn.quasar.dev/img/parallax2.jpg',
    year: 2023,
    technologies: ['React', 'Next.js', 'Tailwind CSS', 'TypeScript'],
    role: 'Lead Développeur sur la partie API. Responsable du design de la base de données. Autonomie totale.',
    interactions: 'Collaboration quotidienne avec un UX Designer sur Figma et feedbacks hebdomadaires.',
    reflexive: 'Ce projet m\'a appris à gérer des flux de données asynchrones complexes.',
  },
  {
    id: 2,
    title: 'Gryphon Academy Website',
    category: 'Web',
    brandColor: '#A855F7',
    description: 'Plateforme e-learning dynamique, du concept au déploiement, incluant des parcours de formation interactifs. Une description un peu plus longue pour tester.',
    image: 'https://cdn.quasar.dev/img/parallax1.jpg',
    year: 2024,
    technologies: ['React', 'Tailwind CSS', 'GSAP', 'Three.js'],
    role: 'Développeur Frontend. Intégration des maquettes Figma et mise en place des animations.',
    interactions: 'Équipe de 3 devs. Daily scrums et Code Reviews croisées.',
    reflexive: 'Maitrise renforcée des animations complexes (GSAP).',
  },
  {
    id: 3,
    title: 'PlayStation – Product Showcase Website',
    category: 'Design',
    brandColor: '#A855F7',
    description: 'Concept interactif moderne mettant en valeur les produits.',
    image: 'https://cdn.quasar.dev/img/mountains.jpg',
    year: 2024,
    technologies: ['React', 'Vite', 'Tailwind CSS', 'JavaScript'],
    role: 'Intégrateur Web & Designer. Création d\'une expérience immersive de A à Z.',
    interactions: 'Travail en totale autonomie.',
    reflexive: 'J\'ai découvert comment lier créativité pure et contraintes de performances.',
  }
])

const filteredProjects = computed(() => {
  if (currentCategory.value === 'All') return projects.value
  return projects.value.filter(p => p.category === currentCategory.value)
})

const openDetails = (project: Project) => {
  selectedProject.value = project
  detailsOpen.value = true
}
</script>

<style scoped>
/* ========================================================== */
/* ALIGNEMENT ET TYPOGRAPHIE                                  */
/* ========================================================== */
.max-width-text { max-width: 700px; }
.line-height-relaxed { line-height: 1.6; }

/* ========================================================== */
/* FILTRES (MINI-NAVBAR)                                      */
/* ========================================================== */
.btn-filter-active { 
  background: #7C3AED !important; 
  color: white !important; 
  border-radius: 6px; 
  font-weight: 500;
  padding: 4px 16px;
}
.btn-filter-inactive { 
  background: rgba(255, 255, 255, 0.05) !important; 
  color: #8A92A3 !important; 
  border-radius: 6px; 
  font-weight: 500;
  padding: 4px 16px;
}

/* ========================================================== */
/* STYLE DES CARTES ET HOMOGÉNÉISATION DES HAUTEURS           */
/* ========================================================== */
.project-card {
  border-radius: 12px;
  background: #111111; 
  border: 1px solid rgba(255, 255, 255, 0.05);
  transition: all 0.3s ease;
  height: 100%; /* S'assure que la carte prend toute la hauteur de la colonne */
}

.project-card:hover {
  transform: translateY(-6px);
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.5);
  border-color: rgba(124, 58, 237, 0.3); 
}

/* Fixer la hauteur de l'image (environ équivalent au ratio 16/9 sur ces largeurs) */
.image-wrapper {
  height: 200px;
  min-height: 200px;
  overflow: hidden;
}

.project-image { 
  transition: transform 0.5s ease; 
  filter: brightness(0.9); 
}
.project-card:hover .project-image { 
  transform: scale(1.03); 
  filter: brightness(1); 
}

/* Fixer une hauteur min pour le titre pour gérer les titres sur 1 ou 2 lignes */
.title-container {
  min-height: 56px; 
}
.title-text {
  line-height: 1.3;
}

/* Fixer une hauteur pour la description (3 lignes max) */
.description-fixed-height {
  height: 66px; /* Ajuste selon ton line-height, ici 3 lignes * 1.6em */
  margin-bottom: 16px;
}

/* Fixer une hauteur pour le conteneur de tags */
.tags-container {
  min-height: 28px; /* Hauteur d'une rangée de chips */
}

/* Le highlight du titre au survol */
.project-card:hover .project-title-transition {
  color: var(--brand-color) !important;
}
.project-title-transition { transition: color 0.3s ease; }

/* ========================================================== */
/* LABELS EXACTEMENT COMME LE SCREEN                          */
/* ========================================================== */
.chip-tech-da {
  background: rgba(124, 58, 237, 0.12) !important; 
  color: #A78BFA !important; 
  border-radius: 16px;
  font-weight: 500;
  padding: 2px 14px;
  font-size: 12px;
}

/* ========================================================== */
/* BOUTONS ACTIONS (OUTLINED)                                 */
/* ========================================================== */
.btn-action-outline { 
  border: 1px solid rgba(255, 255, 255, 0.15) !important; 
  color: #e2e8f0 !important;
  border-radius: 6px;
  font-weight: 500; 
  height: 40px; 
  transition: all 0.3s ease;
}
.btn-action-outline:hover { 
  background: rgba(255, 255, 255, 0.05); 
  border-color: rgba(255, 255, 255, 0.4) !important; 
}

/* ========================================================== */
/* MODALE DARK TECH                                           */
/* ========================================================== */
.modal-dark-tech {
  background: #0B0E14 !important;
  border: 1px solid rgba(255, 255, 255, 0.08);
  border-radius: 20px !important;
}
.bg-header-modal { background: rgba(255, 255, 255, 0.02); }
.modal-body-scroll { max-height: 75vh; }
.border-left-purple { border-left: 3px solid #7C3AED; }
.border-glass { border: 1px solid rgba(255, 255, 255, 0.1); }

.ellipsis-3-lines { display: -webkit-box; -webkit-line-clamp: 3; -webkit-box-orient: vertical; overflow: hidden; }
</style>